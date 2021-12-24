---
layout: home
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
'    <div class="card_preview">'+
'        <img src="[THUMBNAIL]" alt="image" /> '+
'    </div>'+
'    <div class="card_child">'+
'        <div>'+
'        <a href="[LINK]" class="card_header">[HEADER]</a><br>'+
// '        [DESCRIPTION]'+
'        </div>'+
'        <div class="card_footer">'+
'           <div class="card_tags">'+
'           [TAGS]'+
'           </div>'+
'           <div>'+
'           <a href="[LINK]" class="card_readmore">Read More</a>'+
'           </div>'+
'        </div>'+
'    </div>'+
'</div>';

    template = template.replace('[THUMBNAIL]', article.thumbnail);

    template = template.replace('[LINK]', article.link == '' ? 'javascript:void(0)' : article.link);
    template = template.replace('[LINK]', article.link == '' ? 'javascript:void(0)' : article.link);
    template = template.replace('[HEADER]', article.header);
    template = template.replace('[DESCRIPTION]', article.description);
    template = template.replace('[DATE]', article.date);

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
</div> -->

<div id="container">
</div>

<script type="text/javascript">

document.getElementById("blog").classList.add("category_item_selected");

AddArticle({
    header:         'Nodevember 2020 with Amplify Shader Editor',
    description:    'Shaders made without textures',
    link:           'articles/nodevember-2020.html',
    thumbnail:      'images/nodevember-2020/thumb.gif',
    date:           'November 2020',
    tags:           ['shaders']
});
AddArticle({
    header:         'Unity Tips - Build Size And Assets Usage',
    description:    'Quick tip on how to spot what\'s taking up place in your project',
    link:           'articles/tips-build-size.html',
    thumbnail:      'images/tips-build-size/thumb.png',
    date:           'September 2020',
    tags:           ['tips']
});
AddArticle({
    header:         'Shader Breakdown - A Sand Game With Compute Shaders',
    description:    'A version of the classic game running on the GPU',
    link:           'articles/compute-game-of-life.html',
    thumbnail:      'images/compute-game-of-life/thumb.gif',
    date:           'August 2020',
    tags:           ['shaders', 'compute']
});
AddArticle({
    header:         'Shader Breakdown - Simple Outline Post-Process',
    description:    'Pixel-perfect outline for Desktop Garden, our #LD46 jam entry',
    link:           'articles/simple-outline-post-process.html',
    thumbnail:      'images/simple-outline-post-process/thumb.png',
    date:           'April 2020',
    tags:           ['shaders', 'post-process']
});
AddArticle({
    header:         'Shader Project - Uber Shader VFX',
    description:    'Custom shader & inspector to toggle shader features easily',
    link:           'articles/uber-shader-vfx.html',
    thumbnail:      'images/uber-shader-vfx/thumb.gif',
    date:           'March 2020',
    tags:           ['shaders', 'vfx']
});
AddArticle({
    header:         'Shader Breakdown - Voxel Animation Textures',
    description:    'VATs for voxel simulations, from Houdini to Unity using Alembic',
    link:           'articles/voxel-animation-texture.html',
    thumbnail:      'images/voxel-animation-texture/thumb.gif',
    date:           'December 2019',
    tags:           ['shaders', 'houdini', 'vfx']
});
/*AddArticle({
    header:         'Houdini Project - Townscaper\'s grid',
    description:    'Quick attempt in Houdini to generate the grid from Townscaper by Oskar Stålberg',
    link:           '',
    thumbnail:      'images/stalberg-grid/thumb.gif',
    date:           'November 2019',
    tags:           ['houdini']
});*/
AddArticle({
    header:         'Shader Breakdown - Shield Impacts',
    description:    'Pew Pew Pew',
    link:           'articles/shield-impacts.html',
    thumbnail:      'images/shield-impacts/thumb.gif',
    date:           'September 2019',
    tags:           ['shaders', 'vfx']
});
AddArticle({
    header:         'Houdini Tutorial - Sliced Mountains',
    description:    'Godus-inspired islands using heightfields in Houdini',
    link:           'articles/sliced-mountains.html',
    thumbnail:      'images/sliced-mountains/thumb.png',
    date:           'May 2019',
    tags:           ['houdini']
});
AddArticle({
    header:         'Shader Breakdown - Hologram (RTVFX Sketch #18)',
    description:    'GPU Particles, Compute & Geometry shaders',
    link:           'articles/sketch-hologram.html',
    thumbnail:      'images/sketch-hologram/thumb.gif',
    date:           'November 2018',
    tags:           ['shaders', 'vfx', 'compute']
});
// AddArticle({
//     header:         'Shader Project - Parallax Sphere',
//     description:    'Parallax mapping without raymarching',
//     link:           '',
//     thumbnail:      'images/parallax-sphere/sphere.gif',
//     date:           'September 2018',
//     tags:           ['shaders', 'vfx']
// });
</script>
