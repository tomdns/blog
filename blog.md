---
layout: home
pages:
- shield-impacts
---

<script>

var tags = 
{
    'shaders'       : 1,
    'vfx'           : 1,
    'houdini'       : 1,
    'compute'       : 1,
    'tips'          : 1,
    'post-process'  : 1
};

var tagsElements = {};

function ToggleTag(el, tag) {
    tagsElements[tag] = el;
    tags[tag] = 1 - tags[tag];

    if(tags[tag] == 0)
    el.classList.remove('tag_' + tag);
    else
    el.classList.add('tag_' + tag);

    var els = document.getElementsByClassName("card");
    for(var i = 0; i < els.length; i++)
    {
        var children = els[i].getElementsByTagName("span");
        var hide = true;
        for(var j = 0; j < children.length; j++)
        {
            if(tags[children[j].innerHTML] == 1)
            hide = false;
        }

        if(hide) 
        {
            els[i].style.visibility = 'hidden';
            els[i].style.opacity = '0';
            els[i].style.display = 'none';
        }
        else
        {
            els[i].style.visibility = 'visible';
            els[i].style.opacity = '1';
            els[i].style.display = '';
        }
    }

    // var flag = 0;
    // for(const prop in tags)
    // {
    //     if(tags[prop] == 1)
    //     {
    //         flag = 1;
    //         return;
    //     }
    // }

    // if(flag == 0) 
    // {
    //     for(const prop in tags)
    //     {
    //         ToggleTag(tagsElements[prop], prop);
    //     }
    // }
}

function AddArticle(article) {
    var template = 

'<div class="card [EXTRACLASS]">'+
'    <div class="card_child">'+
'        <div>'+
'        <a href="[LINK]" class="card_header">[HEADER]</a><br>'+
'        [DESCRIPTION]'+
'        </div>'+
'    </div>'+
'    <div class="card_preview">'+
'        <img src="[THUMBNAIL]" alt="image" /> '+
'        <p>[DATE]</p> '+
'    </div>'+
'</div>';

    template = template.replace('[THUMBNAIL]', article.thumbnail);
    template = template.replace('[LINK]', article.link == '' ? 'javascript:void(0)' : article.link);
    template = template.replace('[HEADER]', article.header);
    template = template.replace('[DESCRIPTION]', article.description);

    var date = '';
    
    console.log(date);
    
    template = template.replace('[DATE]', date);

    var tags = "";
    if(article.tags)
    {
        for(var i = 0; i < article.tags.length; i++) {
            tags += '<span class="tag ' + ("tag_" + article.tags[i]) + '">'+ article.tags[i] +'</span>';
        }
    }
    
    template = template.replace('[TAGS]', tags);

    var extraClass = "";
    if(article['live'] !== undefined && !article['live']) extraClass = "card_disabled";

    template = template.replace('[EXTRACLASS]', extraClass);

    document.getElementById("container").insertAdjacentHTML('beforeend', template);
}

</script>

<!-- <div id="tags_container">
<span class="tag tag_shaders" onclick="ToggleTag(this, 'shaders')">shaders</span>
<span class="tag tag_vfx" onclick="ToggleTag(this, 'vfx')">vfx</span>
<span class="tag tag_houdini" onclick="ToggleTag(this, 'houdini')">houdini</span>
<span class="tag tag_compute" onclick="ToggleTag(this, 'compute')">compute</span>
<span class="tag tag_tips" onclick="ToggleTag(this, 'tips')">tips</span>
<span class="tag tag_post-process" onclick="ToggleTag(this, 'post-process')">post-process</span>
</div>  -->

<div id="container">

{% assign subpage = site.pages | sort: 'last_update' | reverse | where_exp: "item", "item.url contains 'articles'" %}
{% for item in subpage %}
    <div class="card">
        <div class="card_child">
            <div>
                <a href="{{item.url}}" class="card_header">{{item.title}}</a><br>
                {{item.description}}
            </div>
            <div class="card_date">Last updated {{ item.last_update | item.date | timeago }}</div>
        </div>
        <div class="card_preview">
            <img src="{{item.thumbnail}}" alt="image" />
        </div>
    </div>
{% endfor %}

</div>