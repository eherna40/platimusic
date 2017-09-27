<template lang="pug">
    li 
        h2: a(v-bind:href="artist.url" target="_black") {{ artist.name }}
        div.listeners
            i.material-icons headset
            p {{artist.listeners}}
        img(:src="artist.image[4]['#text']")
        
</template>

<script>
export default {
    name: 'artist',
    props: ['artist']
}
</script>

<style lang="stylus" scoped>
    li
        display block
        margin 10px 10px
        position relative
        overflow hidden
        cursor pointer
        img 
            transition all .5s ease
        .listeners
            position absolute
            z-index 2
            color white
            bottom 20px
            left 20px
            width 100%
            display inline-flex
            opacity 0
            transition all .5s ease
            i 
                background #1e88e5
                border-radius 50%
                height 30px
                width 30px
                color white
                z-index 2
                font-size 20px
                line-height 30px
            p
                margin-left 15px
                font-size 12px
        
    li::after
        content ''
        width 100%
        height 100%
        top 0
        left 0
        position absolute
        overflow hidden
        background rgba(#35495E, 80%)
    li:hover 
        img 
            transform scale(1.3)
        .listeners
            opacity 1
        
    h2
        position absolute
        font-weight 800  
        left 25px
        z-index 1
        top 25px
        a
            color white
            text-decoration none
</style>
