<script>

function AddArticle(article)
{
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
'        <div class="card_footer>'+
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
    template = template.replace('[TAGS]', 'Test');

    document.getElementById("container").insertAdjacentHTML('beforeend', template);

    console.log("Added Article");
}

</script>

## Thomas Denis - Technical Artist

***

<div id="container">
</div>

<script type="text/javascript">
AddArticle({
    header:         'Unity Tips - Build Size And Assets Usage',
    description:    'Quick tip on how to spot what\'s taking up place in your project',
    link:           'articles/tips-build-size.html',
    thumbnail:      'images/tips-build-size/log.png',
    date:           'September 2020'
});
AddArticle({
    header:         'Shader Project - A Sand Game With Compute Shaders',
    description:    'A version of the classic game running on the GPU',
    link:           'articles/compute-game-of-life.html',
    thumbnail:      'images/compute-game-of-life/trees.gif',
    date:           'August 2020'
});
AddArticle({
    header:         'Shader Tutorial - Simple Outline Post-Process',
    description:    'A specific pixel-perfect outline for Desktop Garden, our #LD46 jam entry',
    link:           'articles/simple-outline-post-process.html',
    thumbnail:      'images/simple-outline-post-process/header.png',
    date:           'April 2020'
});
AddArticle({
    header:         'Shader Project - Uber Shader VFX',
    description:    'Custom shader & inspector to toggle shader features easily',
    link:           'articles/uber-shader-vfx.html',
    thumbnail:      'images/uber-shader-vfx/projectiles.gif',
    date:           'March 2020'
});
AddArticle({
    header:         'Shader Project - Voxel Animation Textures',
    description:    'VATs for voxel simulations, from Houdini to Unity using Alembic',
    link:           'articles/voxel-animation-texture.html',
    thumbnail:      'images/voxel-animation-texture/waves.gif',
    date:           'December 2019'
});
AddArticle({
    header:         'Houdini Project - Townscaper\'s grid',
    description:    'Quick attempt in Houdini to generate the grid from Townscaper by Oskar Stålberg',
    link:           'javascript:void(0)',
    thumbnail:      'images/stalberg-grid/process.gif',
    date:           'November 2019'
});
AddArticle({
    header:         'Shader Project - Shield Impacts',
    description:    'An use case of sending an array of values to the shader',
    link:           'articles/shield-impacts.html',
    thumbnail:      'images/shield-impacts/shield.gif',
    date:           'September 2019'
});
AddArticle({
    header:         'Houdini Tutorial - Sliced Mountains',
    description:    'Learn how to generate Godus-inspired islands using heightfields in Houdini',
    link:           'articles/sliced-mountains.html',
    thumbnail:      'images/sliced-mountains/mountain_final.png',
    date:           'May 2019'
});
AddArticle({
    header:         'Shader Project - Hologram (RTVFX Sketch #18)',
    description:    'Project made for the 18th sketch edition on realtimevfx.com. GPU Particles, Compute & Geometry shaders',
    link:           'articles/sketch-hologram.html',
    thumbnail:      'images/sketch-hologram/hologram.gif',
    date:           'November 2018'
});
AddArticle({
    header:         'Shader Project - Parallax Sphere',
    description:    'Parallax mapping without raymarching',
    link:           'javascript:void(0)',
    thumbnail:      'images/parallax-sphere/sphere.gif',
    date:           'September 2018'
});
</script>
