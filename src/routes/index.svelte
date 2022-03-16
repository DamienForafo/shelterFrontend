<script>
    import {onMount} from 'svelte';
    let oldYOffset = 0;
    let newYOffset = 0;
    let topBarClasses = '';
    let topBar;
    let topBarOffsetTop = 0;
    let mainTagDiv;
    let tags;
    let tagsClasses = '';
    let tagsInitialWidth = 500;
    let mainTagWord = '';
    let mainTagExists = false;
    $: mainTagExists = (mainTagWord !== '');
    function handleResize() {
        const mainTagDivWidth = (mainTagExists) ? mainTagDiv.offsetWidth : 0;
        realTags.style.setProperty('--mainTagDivWidth', mainTagDivWidth + 'px');
        tagsClasses = (tagsInitialWidth > document.body.offsetWidth) ? 'fullWidth' : '';
    };
    onMount(() => {
        tags.style.setProperty('--tagsInitialWidth', tagsInitialWidth + 'px')
        topBarOffsetTop = topBar.offsetTop; 
        handleResize();
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


<svelte:window on:scroll={manageScroll} on:resize={handleResize}/>

<div bind:this={topBar} id ="topBar" class={topBarClasses}>
    <div id="topBarBackground"></div>
    <input id="searchInput" type="text" name="searchInput">
    <div id="tags" bind:this={tags} class={tagsClasses}>
        {#if mainTagExists}
        <div id="mainTagDiv" bind:this={mainTagDiv}>
            <div id="backButton"></div>
            <div id="mainTag" class="tag">
                <p>cliqué</p>
            </div>
        </div>
        {/if}
        <div id="realTags">
            <div class="tag">
                <p>coucou</p>
            </div>
            <div class="tag">
                <p>coucou</p>
            </div>
            <div class="tag">
                <p>coucou</p>
            </div>
            <div class="tag">
                <p>coucou</p>
            </div>
            <div class="tag">
                <p>coucou</p>
            </div>
            <div class="tag">
                <p>coucou</p>
            </div>
            <div class="tag">
                <p>coucou</p>
            </div>
            <div class="tag">
                <p>coucou</p>
            </div>
            <div class="tag">
                <p>coucou</p>
            </div>
            <div class="tag">
                <p>coucou</p>
            </div>
            <div class="tag">
                <p>coucou</p>
            </div>
        </div>
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
    :root {
        --topBarHeight: 150px;
        --cardsMargin: 90vh;
        --semiMargin: calc((var(--cardsMargin) - var(--topBarHeight)) / 2);
        --topScroll: 0;
        --tagsPadding: 5px 10px;
        --itemMargin: 0 5px;
    }

    body {
        margin: 0;
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
        top: calc(0px - var(--topBarHeight) - 1px);
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
            z-index: 1;
            position: relative;
            display: flex;
            width: var(--tagsInitialWidth);
            > #mainTagDiv {
                height: 100%;
                background: khaki;
                padding: var(--tagsPadding);
                display: flex;
                justify-content: center;
                align-items: center;
                > #backButton {
                    min-width: 30px;
                    min-height: 30px;
                    background: red;
                    margin: var(--itemMargin);
                }
            }
            > #realTags {
                width: 100%;
                height: 100%;
                padding: var(--tagsPadding);
                display: flex;
                flex-wrap: nowrap;
                align-items: center;
                overflow-x: auto;
                overflow-y: hidden;
                background: blueviolet;
                overflow-x: scroll;
            }
            .tag {
                width: fit-content;
                background: grey;
                border-radius: 30px;
                height: fit-content;
                padding: 5px 10px;
                display: flex;
                justify-content: center;
                align-items: center;
                margin: var(--itemMargin);
                > p {
                    width: fit-content;
                    text-align: center;
                    margin: 0;
                }
            }
            &.fullWidth {
                width: 100%;
                > #realTags {
                    width: calc(100% - var(--mainTagDivWidth));
                }
            }
        }
    }
</style>