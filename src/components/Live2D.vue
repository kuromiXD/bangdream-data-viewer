<template>
  <div ref="viewer">
    <router-link to="/">Back to main</router-link>
  </div>
</template>

<script>
/* global PIXI */
export default {
  name: 'Live2DPage',
  mounted () {
    this.renderer = new PIXI.WebGLRenderer(800, 600)
    this.$refs.viewer.appendChild(this.renderer.view)
    this.stage = new PIXI.Container()

    const modelHaru = {
      'type': 'Live2D Model Setting',
      'name': 'haru',
      'model': 'assets/live2d/chara/001_casual_kasumi.moc.txt',
      'textures':
      [
        'assets/live2d/chara/001_casual_texture_00.png'
      ],
      'physics': 'assets/live2d/chara/001_casual_kasumi.physics.txt',
      'expressions':
      [
        {'name': 'f01', 'file': 'assets/live2d/chara/001_general_f01.exp.txt'},
        {'name': 'f02', 'file': 'assets/live2d/chara/001_general_f02.exp.txt'},
        {'name': 'f03', 'file': 'assets/live2d/chara/001_general_f03.exp.txt'},
        {'name': 'f04', 'file': 'assets/live2d/chara/001_general_f04.exp.txt'}
      ],
      'layout':
      {
        'center_x': 0,
        'y': 1.2,
        'width': 2.9
      },
      'motions':
      {
        'idle':
        [
          {'file': 'assets/live2d/chara/001_general_idle01.mtn.txt', 'fade_in': 2000, 'fade_out': 2000},
          {'file': 'assets/live2d/chara/001_general_idle02.mtn.txt', 'fade_in': 2000, 'fade_out': 2000}
        ]
      }
    }

    const live2dSprite = new PIXI.Live2DSprite(modelHaru)

    this.stage.addChild(live2dSprite)

    live2dSprite.x = -105
    live2dSprite.adjustScale(0, 0, 0.7)
    live2dSprite.adjustTranslate(0.4, 0)
    live2dSprite.startRandomMotion('idle')

    // live2dSprite.on('mousemove', (evt) => {
    //   const point = evt.data.global
    //   live2dSprite.setViewPoint(point.x, point.y)
    // })

    this.animate = () => {
      requestAnimationFrame(this.animate)
      this.renderer.render(this.stage)
    }
    this.animate()
  },
  beforeDestroy () {
    // this.stage.destory()
    this.renderer.destroy()
    Object.keys(PIXI.utils.TextureCache).forEach((texture) => { PIXI.utils.TextureCache[texture].destroy(true) })
  }
}
</script>
