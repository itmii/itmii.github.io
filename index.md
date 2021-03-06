## Bienvenido a la pagina de logica matematica de Michael Pico
## Este proyecto fue posible gracias a a las redes neuronales
https://es.wikipedia.org/wiki/Red_neuronal_artificial
## Que son las redes neuroanles
http://avellano.fis.usal.es/~lalonso/RNA/index.htm
## Cuál es su relacion con la tería de grafoas
http://www.madrimasd.org/blogs/complejidad/2006/10/23/47634
## Que son los conjuntos
https://es.wikipedia.org/wiki/Conjunto
## Cuales son los operadores logicos
https://fmhelp.filemaker.com/help/18/fmp/es/index.html#page/FMP_Help/logical-operators.html
Incluir imagenes

<img src="https://www.ecured.cu/images/e/e4/Operadores_logicos.png">
<img src="https://andromedavaluecapital.com/wp-content/uploads/2018/02/neuronal-network-1024x585.jpg" alt="Red neuronal">
<img src="https://i.ytimg.com/vi/a_tXDYOiqvI/maxresdefault.jpg">
![Grafo](https://www.madrimasd.org/blogs/matematicas/files/2012/09/Network_representation_of_brain_connectivity.jpg)




![Grafo](https://www.madrimasd.org/blogs/matematicas/files/2012/09/Network_representation_of_brain_connectivity.jpg)
<script src="https://www.gstatic.com/dialogflow-console/fast/messenger/bootstrap.js?v=1"></script>
<df-messenger
  chat-title="AGENTE_LOGICA"
  agent-id="bc6774a5-1a9c-4198-a04d-dc598e8a9ab0"
  language-code="en"
></df-messenger>

<div>Teachable Machine Image Model</div>
<button type="button" onclick="init()">Start</button>
<div id="webcam-container"></div>
<div id="label-container"></div>
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@1.3.1/dist/tf.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/@teachablemachine/image@0.8/dist/teachablemachine-image.min.js"></script>
<script type="text/javascript">
    // More API functions here:
    // https://github.com/googlecreativelab/teachablemachine-community/tree/master/libraries/image

    // the link to your model provided by Teachable Machine export panel
    const URL = "https://teachablemachine.withgoogle.com/models/V-im73h60/";

    let model, webcam, labelContainer, maxPredictions;

    // Load the image model and setup the webcam
    async function init() {
        const modelURL = URL + "model.json";
        const metadataURL = URL + "metadata.json";

        // load the model and metadata
        // Refer to tmImage.loadFromFiles() in the API to support files from a file picker
        // or files from your local hard drive
        // Note: the pose library adds "tmImage" object to your window (window.tmImage)
        model = await tmImage.load(modelURL, metadataURL);
        maxPredictions = model.getTotalClasses();

        // Convenience function to setup a webcam
        const flip = true; // whether to flip the webcam
        webcam = new tmImage.Webcam(200, 200, flip); // width, height, flip
        await webcam.setup(); // request access to the webcam
        await webcam.play();
        window.requestAnimationFrame(loop);

        // append elements to the DOM
        document.getElementById("webcam-container").appendChild(webcam.canvas);
        labelContainer = document.getElementById("label-container");
        for (let i = 0; i < maxPredictions; i++) { // and class labels
            labelContainer.appendChild(document.createElement("div"));
        }
    }

    async function loop() {
        webcam.update(); // update the webcam frame
        await predict();
        window.requestAnimationFrame(loop);
    }

    // run the webcam image through the image model
    async function predict() {
        // predict can take in an image, video or canvas html element
        const prediction = await model.predict(webcam.canvas);
        for (let i = 0; i < maxPredictions; i++) {
            const classPrediction =
                prediction[i].className + ": " + prediction[i].probability.toFixed(2);
            labelContainer.childNodes[i].innerHTML = classPrediction;
        }
    }
</script>
