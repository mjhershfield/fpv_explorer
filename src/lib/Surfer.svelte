<script>
    import init, * as bindings from '../surfer/surfer-843a90cae0b7c1cc.js';

    let wasm;
    init('../surfer/surfer-843a90cae0b7c1cc_bg.wasm').then(res => {
        wasm = res;
        console.log(wasm);
        dispatchEvent(new CustomEvent("TrunkApplicationStarted", {detail: {wasm}}));
        register_message_listener()
    });

    window.wasmBindings = bindings;

    function on_surfer_error(msg) {
        console.log("Setting error message")
        document.getElementById("error_message").innerHTML = msg
        document.getElementById("error_container").style.display = "block"
    }

    window.on_surfer_error = on_surfer_error;
</script>

<link rel="manifest" href="manifest.json">
<meta name="theme-color" media="(prefers-color-scheme: light)" content="white">
<meta name="theme-color" media="(prefers-color-scheme: dark)" content="#404040">
<link rel="modulepreload" href="./surfer/surfer-843a90cae0b7c1cc.js">
<link rel="preload" href="./surfer/surfer-843a90cae0b7c1cc_bg.wasm" crossorigin=anonymous integrity="sha384-X4PH2AIwOjEvLkmR6x2wtMaAYNA9BfvKlxdVAF0KmCm3lNDOTNEVopH6Foh9SPqI" as="fetch" type="application/wasm">
<link rel="script" href = "./surfer/integration.js">

        <!--<style>
        html {
            /* Remove touch delay: */
            touch-action: manipulation;
        }

        body {
            /* Light mode background color for what is not covered by the egui canvas,
            or where the egui canvas is translucent. */
            background: #909090;
        }

        @media (prefers-color-scheme: dark) {
            body {
                /* Dark mode background color for what is not covered by the egui canvas,
                or where the egui canvas is translucent. */
                background: #404040;
            }
        }

        /* Allow canvas to fill entire web page: */

        /* Make canvas fill entire document: */
        canvas {
            margin-right: auto;
            margin-left: auto;
            display: block;
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
        }

        .centered {
            margin-right: auto;
            margin-left: auto;
            display: block;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            color: #f0f0f0;
            font-size: 24px;
            font-family: Ubuntu-Light, Helvetica, sans-serif;
            text-align: center;
        }

        /* ---------------------------------------------- */
        /* Loading animation from https://loading.io/css/ */
        .lds-dual-ring {
            display: inline-block;
            width: 24px;
            height: 24px;
        }

        .lds-dual-ring:after {
            content: " ";
            display: block;
            width: 24px;
            height: 24px;
            margin: 0px;
            border-radius: 50%;
            border: 3px solid #fff;
            border-color: #fff transparent #fff transparent;
            animation: lds-dual-ring 1.2s linear infinite;
        }

        @keyframes lds-dual-ring {
            0% {
                transform: rotate(0deg);
            }

            100% {
                transform: rotate(360deg);
            }
        }

        #error_container {
            padding: 1em;
            border-radius: 0.5em;
            margin: 0px auto;
            max-width: 980px;
            color: #ffffff;
            background-color: black;
            position: relative;
            height: 90%;
            overflow: scroll;
        }

        #error_container a {
            color: #ff9999;
        }

        #error_message {
            overflow: scroll;
            white-space: break-spaces;
        }
    </style> -->


<div>
    <!-- The WASM code will resize the canvas dynamically -->
    <!-- the id is hardcoded in main.rs . so, make sure both match. -->
    <canvas id="the_canvas_id"></canvas>

    <div id="error_container" style="display: none;">
        <h1>Sorry, Surfer crashed 🔥</h1>
        <p>
            Something caused Surfer to crash. Please report the error on
            <a href="https://gitlab.com/surfer-project/surfer/-/issues/new">
                gitlab
            </a>
        </p>
        <p>
            Any report is appreciated, but it is extra helpful if you can attach the waveform that caused
            the crash and/or the steps to reproduce the crash.
        </p>
        <h3>
            Backtrace:
        </h3>
        <div class="error_container">
            <!-- This is filled in by javascript -->
            <code id="error_message"></code>
        </div>
    </div>


    <!--Register Service Worker. this will cache the wasm / js scripts for offline use (for PWA functionality). -->
    <!-- Force refresh (Ctrl + F5) to load the latest files instead of cached files
    <script>
        // We disable caching during development so that we always view the latest version.
        if ('serviceWorker' in navigator && window.location.hash !== "#dev") {
            window.addEventListener('load', function () {
                navigator.serviceWorker.register('sw.js');
            });
        }
    </script> -->
</div>
