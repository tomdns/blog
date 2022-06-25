---
layout: home
---

<script>
document.getElementById("work").classList.add("category_item_selected");
</script>

<script>
function AddVideo(path, url) {

    var template = 
'<div class="work_item">'+
'        <a href=[URL]><video autoplay muted loop>'+
'            <source src="[VIDEO]" type="video/mp4" />'+
'        </video></a>'+
'</div>';

    template = template.replace('[VIDEO]', path);
    template = template.replace('[URL]', url !== undefined ? '"' + url + ' ' + '" target="_blank"' : '');

    document.getElementById("grid").insertAdjacentHTML('beforeend', template);
}
</script>

# Hi! 👋

<div id="article-content">
    My name is Thomas Denis. I'm a technical artist focused on visual effects, shaders, tools and procedural generation. I write tech articles from time to time, you can read them <a href="./blog.html">here</a> !
</div>


<div id="container">
    <div id="grid" class="work_grid">
    </div>
</div>

<script type="text/javascript">
    AddVideo("images/work/vfx_combo.mp4", "https://www.artstation.com/artwork/mzdzRE");
    AddVideo("images/work/shield_v2.mp4");
    // AddVideo("images/work/fishies.mp4");
    AddVideo("images/work/gpuparticles_plexus.mp4");
    AddVideo("images/work/vfx_trails.mp4");
    // AddVideo("images/work/gpuparticles_comet.mp4");
    // AddVideo("images/work/shockwave2.mp4");
    AddVideo("images/work/shield.mp4");
    AddVideo("images/work/vfx_aura.mp4");
    // AddVideo("images/work/projectiles.mp4");
    AddVideo("images/work/breached.mp4");
    AddVideo("images/work/vfx_shield.mp4");
    AddVideo("images/work/voxel_explosion.mp4");
    AddVideo("images/work/seaway.mp4");
    AddVideo("images/work/sphere.mp4");
    AddVideo("images/work/hologram_turnaround.mp4");
</script>