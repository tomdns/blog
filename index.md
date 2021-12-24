---
layout: home
---

<script>
function AddVideo(path) {

    var template = 
'<div class="work_item">'+
'        <video autoplay muted loop>'+
'            <source src="[VIDEO]" type="video/mp4" />'+
'        </video>'+
'</div>';

    template = template.replace('[VIDEO]', path);

    document.getElementById("grid").insertAdjacentHTML('beforeend', template);
}
</script>

<div id="grid" class="work_grid">
</div>

<script type="text/javascript">
    AddVideo("images/work/shield_v2.mp4");
    AddVideo("images/work/fishies.mp4");
    AddVideo("images/work/gpuparticles_plexus.mp4");
    AddVideo("images/work/vfx_trails.mp4");
    AddVideo("images/work/gpuparticles_comet.mp4");
    AddVideo("images/work/shield.mp4");
    AddVideo("images/work/shockwave.mp4");
    AddVideo("images/work/vfx_aura.mp4");
    AddVideo("images/work/projectiles.mp4");
    AddVideo("images/work/breached.mp4");
    AddVideo("images/work/vfx_shield.mp4");
    AddVideo("images/work/voxel_explosion.mp4");
    AddVideo("images/work/seaway.mp4");
    AddVideo("images/work/sphere.mp4");
    AddVideo("images/work/hologram_turnaround.mp4");
</script>