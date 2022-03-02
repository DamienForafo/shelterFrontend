<script>
    import {onMount} from 'svelte';
    let oldYOffset = 0;
    let newYOffset = 0;
    let topBarClasses = '';
    let topBar;
    let topBarOffsetTop = 0;
    onMount(() => {
        topBarOffsetTop = topBar.offsetTop;
    });
    function manageScroll(e) {
        document.body.style.setProperty('--scroll', window.pageYOffset / (document.body.offsetHeight - window.innerHeight)); // % of the page
        document.body.style.setProperty('--topScroll', (window.pageYOffset - topBarOffsetTop) / topBarOffsetTop); // % of the height between topBar & cards
        oldYOffset = newYOffset;
        newYOffset = window.pageYOffset;
        if (oldYOffset < newYOffset) topBarClasses = '';
        else topBarClasses = 'show';
    }
</script>


<svelte:window on:scroll={manageScroll}/>

<div bind:this={topBar} id ="topBar" class={topBarClasses}>
    <div id="topBarBackground"></div>
    <input id="searchInput" type="text" name="searchInput">
    <div id="tags">

    </div>
</div>


<div id="cards"> <!--à virer-->
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

<style global lang="less">
    body {
        margin: 0;
        --topBarHeight: 120px;
        --cardsMargin: 90vh;
        --semiMargin: calc(~"(var(--cardsMargin) - var(--topBarHeight)) / 2");
    }

    #cards {
        width: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        flex-wrap: wrap;
        margin-top: var(--semiMargin);
    }

    .carte {
        width: 300px;
        height: 300px;
        background: #c8d8f0;
        margin: 30px;
    }

    #topBar {
        position: -webkit-sticky;
        position: sticky;
        top: calc(~"0px - var(--topBarHeight) - 1px");
        margin-top: var(--semiMargin);
        left: 0;
        width : 100%;
        height: var(--topBarHeight);
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        transition: top 0.15s;
        z-index: 1;
        > #topBarBackground {
            position: absolute;
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            background: #b886bb;
            opacity: var(--topScroll);
        }
        &.show {
            top: -1px;
        }
        input {
            height: 40px;
            margin-bottom: 10px;
            z-index: 1;
        }
        #tags {
            width: 200px;
            height: 40px;
            background: blueviolet;
            z-index: 1;
        }
    }
</style>