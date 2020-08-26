<script>
    export let name;

    let bits = [8, 4, 2, 1];

    let binaryClock = {
        hours: {
            10: [0, 0],
            1: [0, 0, 0, 0]
        },
        minutes: {
            10: [0, 0, 0],
            1: [0, 0, 0, 0]
        },
        seconds: {
            10: [0, 0, 0],
            1: [0, 0, 0, 0]
        }
    }
    let now = new Date();

    setInterval(() => {
        refresh()
    }, 1000);

    function refresh() {
        now = new Date();
        setBinaryTime(now.getHours(), "hours");
        setBinaryTime(now.getMinutes(), "minutes");
        setBinaryTime(now.getSeconds(), "seconds");
    }

    function setBinaryTime(time, hand) {

        let oneBits = (time % 10);

        for (let i = 0; i < binaryClock[hand]["1"].length; i++) {
            binaryClock[hand]["1"][i] = oneBits & 1;
            oneBits >>= 1;
        }

        let tenBits = time / 10;

        for (let i = 0; i < binaryClock[hand]["10"].length; i++) {
            binaryClock[hand]["10"][i] = tenBits & 1;
            tenBits >>= 1;
        }
    }

</script>

<main>
    { now.getHours() } : { now.getMinutes() } : { now.getSeconds() }
    <div class="container">
        <table border="0">
            <tr>
                <td></td>
                {#each Object.keys(binaryClock) as hand}
                    <th>{hand}</th>
                {/each}
            </tr>

            <tr>
                <td></td>
                {#each {length: 3} as _}
                    <td>
                        <table class="innertable">
                            <tr>
                                <th>10</th>
                                <th>1</th>
                            </tr>
                        </table>
                    </td>
                {/each}
            </tr>

            {#each bits as bit, i}
                <tr>
                    <td>{bit}</td>
                    {#each Object.keys(binaryClock) as hand}
                        <td>
                            <table class="innertable">
                                {#if binaryClock[hand]["10"][3-i] === undefined}
                                    <td></td>
                                {:else}
                                    <td>{binaryClock[hand]["10"][3-i]}</td>
                                {/if}
                                <td>{binaryClock[hand]["1"][3-i]}</td>
                            </table>
                        </td>
                    {/each}
                </tr>
            {/each}

        </table>
    </div>
</main>

<style>
    .container {
        display: flex;
        justify-content: center;
        padding: 50px;
    }

    td {
        min-width: 20px;
    }

    table {
    }

    .innertable {
        margin-left: auto;
        margin-right: auto;
    }

    .innertable td {
        border: 1px solid black;
    }

    main {
        text-align: center;
        padding: 1em;
        max-width: 240px;
        margin: 0 auto;
    }

    h1 {
        color: #ff3e00;
        text-transform: uppercase;
        font-size: 4em;
        font-weight: 100;
    }

    @media (min-width: 640px) {
        main {
            max-width: none;
        }
    }
</style>