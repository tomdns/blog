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

function ToggleTag(el, tag) {
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
            els[i].style.display = 'none';
            console.log(els[i]);
        }
        else
        {
            els[i].style.display = '';
        }
    }

    console.log("Toggled " + tag);
}

function AddArticle(article) {
    var template = 

'<div class="card">'+
'    <div>'+
'        <img src="[THUMBNAIL]" alt="image" class="card_preview" /> '+
'    </div>'+
'    <div class="card_child">'+
'        <div>'+
'        <a href="[LINK]">[HEADER]</a><br>'+
'        [DESCRIPTION]'+
'        </div>'+
'        <div class="card_footer">'+
'           <div class="card_tags">'+
'           [TAGS]'+
'           </div>'+
'           <div class="card_date">'+
'           [DATE]'+
'           </div>'+
'        </div>'+
'    </div>'+
'</div>';

    template = template.replace('[THUMBNAIL]', article.thumbnail);
    template = template.replace('[LINK]', article.link);
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

    document.getElementById("container").insertAdjacentHTML('beforeend', template);
}

</script>

## Thomas Denis - Technical Artist

***

<div id="tags_container">
<span class="tag tag_shaders" onclick="ToggleTag(this, 'shaders')">shaders</span>
<span class="tag tag_vfx" onclick="ToggleTag((this, 'vfx')">vfx</span>
<span class="tag tag_houdini" onclick="ToggleTag((this, 'houdini')">houdini</span>
<span class="tag tag_compute" onclick="ToggleTag((this, 'compute')">compute</span>
<span class="tag tag_tips" onclick="ToggleTag((this, 'tips')">tips</span>
<span class="tag tag_post-process" onclick="ToggleTag((this, 'post-process')">post-process</span>
</div>

<div id="container">
</div>

<script type="text/javascript">
AddArticle({
    header:         'Unity Tips - Build Size And Assets Usage',
    description:    'Quick tip on how to spot what\'s taking up place in your project',
    link:           'articles/tips-build-size.html',
    thumbnail:      'images/tips-build-size/log.png',
    date:           'September 2020',
    tags:           ['tips']
});
AddArticle({
    header:         'Shader Project - A Sand Game With Compute Shaders',
    description:    'A version of the classic game running on the GPU',
    link:           'articles/compute-game-of-life.html',
    thumbnail:      'images/compute-game-of-life/trees.gif',
    date:           'August 2020',
    tags:           ['shaders', 'compute']
});
AddArticle({
    header:         'Shader Tutorial - Simple Outline Post-Process',
    description:    'A specific pixel-perfect outline for Desktop Garden, our #LD46 jam entry',
    link:           'articles/simple-outline-post-process.html',
    thumbnail:      'images/simple-outline-post-process/header.png',
    date:           'April 2020',
    tags:           ['shaders', 'post-process']
});
AddArticle({
    header:         'Shader Project - Uber Shader VFX',
    description:    'Custom shader & inspector to toggle shader features easily',
    link:           'articles/uber-shader-vfx.html',
    thumbnail:      'images/uber-shader-vfx/projectiles.gif',
    date:           'March 2020',
    tags:           ['shaders', 'vfx']
});
AddArticle({
    header:         'Shader Project - Voxel Animation Textures',
    description:    'VATs for voxel simulations, from Houdini to Unity using Alembic',
    link:           'articles/voxel-animation-texture.html',
    thumbnail:      'images/voxel-animation-texture/waves.gif',
    date:           'December 2019',
    tags:           ['shaders', 'houdini', 'vfx']
});
AddArticle({
    header:         'Houdini Project - Townscaper\'s grid',
    description:    'Quick attempt in Houdini to generate the grid from Townscaper by Oskar Stålberg',
    link:           'javascript:void(0)',
    thumbnail:      'images/stalberg-grid/process.gif',
    date:           'November 2019',
    tags:           ['houdini']
});
AddArticle({
    header:         'Shader Project - Shield Impacts',
    description:    'An use case of sending an array of values to the shader',
    link:           'articles/shield-impacts.html',
    thumbnail:      'images/shield-impacts/shield.gif',
    date:           'September 2019',
    tags:           ['shaders', 'vfx']
});
AddArticle({
    header:         'Houdini Tutorial - Sliced Mountains',
    description:    'Learn how to generate Godus-inspired islands using heightfields in Houdini',
    link:           'articles/sliced-mountains.html',
    thumbnail:      'images/sliced-mountains/mountain_final.png',
    date:           'May 2019',
    tags:           ['houdini']
});
AddArticle({
    header:         'Shader Project - Hologram (RTVFX Sketch #18)',
    description:    'Project made for the 18th sketch edition on realtimevfx.com. GPU Particles, Compute & Geometry shaders',
    link:           'articles/sketch-hologram.html',
    thumbnail:      'images/sketch-hologram/hologram.gif',
    date:           'November 2018',
    tags:           ['shaders', 'vfx', 'compute']
});
AddArticle({
    header:         'Shader Project - Parallax Sphere',
    description:    'Parallax mapping without raymarching',
    link:           'javascript:void(0)',
    thumbnail:      'images/parallax-sphere/sphere.gif',
    date:           'September 2018',
    tags:           ['shaders', 'vfx']
});
</script>
