---
layout: home
---

<script>
document.getElementById("blog").classList.add("category_item_selected");
</script>

<script>

var tags = 
{
    'shaders'       : 1,
    'vfx'           : 1,
    'houdini'       : 1,
    'tips'          : 1,
    'post-process'  : 1
};

function ToggleAll() {
    for(var key in tags)
    {
        tags[key] = 1;
    }  

    var elements = document.getElementsByClassName("tag");
    for(var j = 0; j < elements.length; j++)
    {
        if(!elements[j].classList.contains('tag_selected'))
        {
            elements[j].classList.add('tag_selected');
        }
    }

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
}

function ToggleTag(el, tag) {

    for(var key in tags)
    {
        tags[key] = 0;
    }  

    var elements = document.getElementsByClassName("tag");
    for(var j = 0; j < elements.length; j++)
    {
        for(var i = elements[j].classList.length - 1; i >= 0; i--) 
        {
            if(elements[j].classList[i] == 'tag_selected') 
            {
                elements[j].classList.remove(elements[j].classList[i]);
            }
        }
    }

    tags[tag] = 1;
    el.classList.add('tag_selected');
    // else
    // {
    //     tags[tag] = 1 - tags[tag];

    //     if(tags[tag] == 0)
    //         el.classList.remove('tag_selected');
    //     else
    //     {
    //         el.classList.add('tag_selected');
    //     }
    // }

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
}

</script>

<div id="menu_container">
    <div id="tags_container">
        <span class="tag tag_selected" onclick="ToggleTag(this, 'shaders')">shaders</span>
        <span class="tag tag_selected" onclick="ToggleTag(this, 'vfx')">vfx</span>
        <span class="tag tag_selected" onclick="ToggleTag(this, 'houdini')">houdini</span>
        <span class="tag tag_selected" onclick="ToggleTag(this, 'tips')">tips</span>
        <span class="tag tag_selected" onclick="ToggleTag(this, 'post-process')">post-process</span> 
        <span class="tag tag_selected" onclick="ToggleAll()">x</span>
    </div>  
    <div>
        <input id="search" type="text" placeholder="Search article..." name="search">
    </div> 
</div>  


<div id="container">

{% assign subpage = site.pages | sort: 'last_update' | reverse | where_exp: "item", "item.url contains 'articles'" %}
{% for item in subpage %}
    <div class="card">
        <div class="card_child">
            <div>
                <a href="{{item.url}}" class="card_header">{{item.title}}</a>
            </div>  
            <div>
            {% for tag in item.tags %}
                <span class="tag_article">{{tag}}</span>  
            {% endfor %}
            </div>
            <!-- <div class="card_date">
                 Last updated {{ item.last_update }}
            </div> -->
        </div>
        <div class="card_preview">
            <img src="{{item.thumbnail}}" alt="image" />
        </div>
    </div>
{% endfor %}

</div>

<script>

var els = document.getElementsByClassName("card");
var titles = document.getElementsByClassName("card_header");
setInterval(function() { 
    let val = document.getElementById("search").value;
    for(var i = 0; i < els.length; i++)
    {
        var children = els[i].getElementsByTagName("span");
        var hide = true;
        for(var j = 0; j < children.length; j++)
        {
            if(tags[children[j].innerHTML] == 1)
            hide = false;
        }

        if(val != '')
        if(!titles[i].innerHTML.toLowerCase().includes(val.toLowerCase())) 
        {
            hide = true;
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

}, 100);
</script>