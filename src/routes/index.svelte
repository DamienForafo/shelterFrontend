<script>
    let oldValue = 0
    let newValue = 0
    let topBarClasses = 'coucou';
    function hideTopBar(e) {
        console.log('scroll');
        oldValue = newValue;
        newValue = window.pageYOffset;
        if (oldValue < newValue) {
            topBarClasses = 'hidden';
        }
        else if (oldValue > newValue) {
            topBarClasses = '';
        }
    }
</script>



<svelte:window on:scroll={hideTopBar}/>


<div id ="topBar" class={topBarClasses}>
    <button id="menuButton">

    </button>
    <input id="searchInput" type="text" name="searchInput">
</div>


<div id="bidon"> <!--à virer-->
    <div class="carte"></div>
    <div class="carte"></div>
    <div class="carte"></div>
    <div class="carte"></div>
    <div class="carte"></div>
    <div class="carte"></div>
    <div class="carte"></div>
    <div class="carte"></div>
    <div class="carte"></div>
    <div class="carte"></div>
    <div class="carte"></div>
    <div class="carte"></div>
    <div class="carte"></div>
    <div class="carte"></div>
    <div class="carte"></div>
    <div class="carte"></div>
    <div class="carte"></div>
    <div class="carte"></div>
    <div class="carte"></div>
    <div class="carte"></div>
</div>




<style lang="less">
    :root {
        --topBarHeight: 50px;
    }

    #bidon {
        display: flex;
        justify-content: center;
        align-items: center;
        flex-wrap: wrap;
        margin-top: 200px;
    }

    .carte {
        width: 300px;
        height: 300px;
        background: darkcyan;
        margin: 30px;
    }

    #topBar {
        position: fixed;
        top: 0;
        left: 0;
        background: seagreen;
        width : 100%;
        height: var(--topBarHeight);
        display: flex;
        justify-content: center;
        align-items: center;
        transition: top 0.15s;
        &.hidden {
            top: calc(0px - var(--topBarHeight) - 1px);
        }
    }
    #topBar.hidden {
         top: calc(0px - var(--topBarHeight) - 1px);
    }

    #menuButton {
        --menuButtonWidth: 30px;
        width: var(--menuButtonWidth);
        height: var(--menuButtonWidth);
        position: absolute;
        left: calc((var(--topBarHeight) - var(--menuButtonWidth)) / 2);
    }
</style>