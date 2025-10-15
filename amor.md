---
layout: blank
title: Mensagem Especial
---

{% raw %}
<style>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }

    body {
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        background: linear-gradient(135deg, #4169E1 0%, #87CEEB 100%);
        min-height: 100vh;
        overflow: hidden;
        position: relative;
    }

    .container {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        min-height: 100vh;
        position: relative;
        z-index: 1;
    }

    .title {
        color: white;
        font-size: 3.5rem;
        font-weight: 700;
        text-align: center;
        margin-bottom: 2rem;
        text-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
        opacity: 0;
        animation: fadeInDown 1s ease-out 0.5s forwards;
    }

    .subtitle {
        color: rgba(255, 255, 255, 0.9);
        font-size: 1.5rem;
        text-align: center;
        margin-bottom: 3rem;
        text-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
        opacity: 0;
        animation: fadeInUp 1s ease-out 0.8s forwards;
        max-width: 800px;
        padding: 0 2rem;
    }

    #canvas-container {
        width: 100%;
        height: 300px;
        display: flex;
        justify-content: center;
        align-items: center;
        margin-bottom: 3rem;
    }

    canvas {
        cursor: pointer;
    }

    .question-container {
        opacity: 0;
        animation: fadeIn 1s ease-out 3s forwards;
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 1.5rem;
        margin-bottom: 2rem;
    }

    .question-text {
        color: white;
        font-size: 1.3rem;
        text-align: center;
        text-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
        padding: 0 2rem;
    }

    .input-group {
        display: flex;
        gap: 1rem;
        align-items: center;
    }

    .answer-input {
        padding: 1rem 1.5rem;
        font-size: 1.1rem;
        border: 3px solid rgba(255, 255, 255, 0.3);
        border-radius: 12px;
        background: rgba(255, 255, 255, 0.15);
        backdrop-filter: blur(10px);
        color: white;
        outline: none;
        transition: all 0.3s ease;
        min-width: 300px;
        text-align: center;
    }

    .answer-input::placeholder {
        color: rgba(255, 255, 255, 0.6);
    }

    .answer-input:focus {
        border-color: rgba(255, 255, 255, 0.8);
        background: rgba(255, 255, 255, 0.25);
        box-shadow: 0 0 20px rgba(135, 206, 235, 0.5);
    }

    .submit-btn {
        padding: 1rem 2.5rem;
        font-size: 1.1rem;
        font-weight: 600;
        border: none;
        border-radius: 12px;
        background: rgba(255, 255, 255, 0.9);
        color: #4169E1;
        cursor: pointer;
        transition: all 0.3s ease;
        box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
    }

    .submit-btn:hover {
        background: white;
        transform: translateY(-2px);
        box-shadow: 0 6px 20px rgba(0, 0, 0, 0.3);
    }

    .submit-btn:active {
        transform: translateY(0);
    }

    .error-message {
        color: #ff6b6b;
        background: rgba(255, 255, 255, 0.9);
        padding: 0.8rem 1.5rem;
        border-radius: 8px;
        font-size: 1rem;
        opacity: 0;
        transition: opacity 0.3s ease;
        text-align: center;
    }

    .error-message.show {
        opacity: 1;
    }

    .success-message {
        position: fixed;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        color: white;
        font-size: 1.5rem;
        line-height: 1.8;
        font-weight: 400;
        text-align: center;
        z-index: 100;
        opacity: 0;
        text-shadow: 0 2px 20px rgba(0, 0, 0, 0.5);
        background: rgba(65, 105, 225, 0.3);
        backdrop-filter: blur(20px);
        padding: 3rem;
        border-radius: 20px;
        border: 2px solid rgba(255, 255, 255, 0.2);
        max-width: 90%;
        max-height: 80vh;
        overflow-y: auto;
        box-shadow: 0 10px 40px rgba(0, 0, 0, 0.3);
    }

    .success-message.show {
        animation: successAppear 0.8s ease-out forwards;
    }

    @keyframes fadeInDown {
        from {
            opacity: 0;
            transform: translateY(-50px);
        }
        to {
            opacity: 1;
            transform: translateY(0);
        }
    }

    @keyframes fadeInUp {
        from {
            opacity: 0;
            transform: translateY(50px);
        }
        to {
            opacity: 1;
            transform: translateY(0);
        }
    }

    @keyframes fadeIn {
        to { opacity: 1; }
    }

    @keyframes successAppear {
        0% {
            opacity: 0;
            transform: translate(-50%, -50%) scale(0.8);
        }
        100% {
            opacity: 1;
            transform: translate(-50%, -50%) scale(1);
        }
    }

    @media (max-width: 768px) {
        .title {
            font-size: 2.5rem;
        }
        .subtitle {
            font-size: 1.2rem;
        }
        .answer-input {
            min-width: 250px;
            font-size: 1rem;
        }
        .input-group {
            flex-direction: column;
        }
        .success-message {
            font-size: 1.2rem;
            padding: 2rem;
        }
    }
</style>

<div class="container">
    <h1 class="title">Espero que tenha gostado da surpresa</h1>
    <p class="subtitle">Mas, ainda não acabou. Tem mais o que gostaria de te dizer, mas pensei em... ser mais discreto :)</p>
    <div id="canvas-container"></div>
        <div class="question-container">
            <p class="question-text">Por isso, antes de continuarmos me responda: Qual a senha?</p>
            <div class="input-group">
                <input type="text" class="answer-input" id="answerInput" placeholder="Digite sua resposta...">
                <button class="submit-btn" id="submitBtn">Verificar</button>
            </div>
            <div class="error-message" id="errorMessage">Resposta incorreta. Tente novamente!</div>
        </div>  
    </div> 
</div>

<div class="success-message" id="successMessage"></div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
<script>
    function xorEncrypt(text, key) {
        let result = '';
        for (let i = 0; i < text.length; i++) {
            result += String.fromCharCode(text.charCodeAt(i) ^ key.charCodeAt(i % key.length));
        }
        return btoa(result);
    }

    function xorDecrypt(encoded, key) {
        try {
            const text = atob(encoded);
            let result = '';
            for (let i = 0; i < text.length; i++) {
                result += String.fromCharCode(text.charCodeAt(i) ^ key.charCodeAt(i % key.length));
            }
            return result;
        } catch (e) {
            return null;
        }
    }

    // GERE SEU CONTEÚDO CRIPTOGRAFADO AQUI
    const encryptedContent = "SUA_STRING_CRIPTOGRAFADA_AQUI";

    const answerInput = document.getElementById('answerInput');
    const submitBtn = document.getElementById('submitBtn');
    const errorMessage = document.getElementById('errorMessage');
    const successMessage = document.getElementById('successMessage');

    function normalizeAnswer(answer) {
        return answer.toLowerCase().trim();
    }

    function isValidText(text) {
        if (!text || text.length === 0) return false;
        
        let validChars = 0;
        let totalChars = text.length;
        
        for (let i = 0; i < text.length; i++) {
            const code = text.charCodeAt(i);
            if ((code >= 32 && code <= 126) || code >= 160 || code === 10 || code === 13) {
                validChars++;
            }
        }
        
        return (validChars / totalChars) >= 0.9;
    }

    function verifyAnswer() {
        const userAnswer = normalizeAnswer(answerInput.value);
        
        if (!userAnswer) {
            showError('Por favor, digite uma resposta!');
            return;
        }

        const decrypted = xorDecrypt(encryptedContent, userAnswer);
        
        if (decrypted && isValidText(decrypted)) {
            showSuccess(decrypted);
        } else {
            showError('Resposta incorreta. Tente novamente!');
            answerInput.value = '';
            answerInput.focus();
        }
    }

    function showError(message) {
        errorMessage.textContent = message;
        errorMessage.classList.add('show');
        answerInput.style.borderColor = '#ff6b6b';
        
        setTimeout(() => {
            errorMessage.classList.remove('show');
            answerInput.style.borderColor = 'rgba(255, 255, 255, 0.3)';
        }, 3000);
    }

    function showSuccess(content) {
        successMessage.innerHTML = content;
        successMessage.classList.add('show');
        document.querySelector('.question-container').style.display = 'none';
    }

    submitBtn.addEventListener('click', verifyAnswer);
    answerInput.addEventListener('keypress', (e) => {
        if (e.key === 'Enter') {
            verifyAnswer();
        }
    });

    // THREE.JS
    const container = document.getElementById('canvas-container');
    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(75, container.clientWidth / container.clientHeight, 0.1, 1000);
    const renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
    
    renderer.setSize(container.clientWidth, container.clientHeight);
    container.appendChild(renderer.domElement);

    const materials = [
        new THREE.MeshPhongMaterial({ color: 0x4169E1, transparent: true, opacity: 0.9, shininess: 100 }),
        new THREE.MeshPhongMaterial({ color: 0x87CEEB, transparent: true, opacity: 0.9, shininess: 100 }),
        new THREE.MeshPhongMaterial({ color: 0x5B8FE8, transparent: true, opacity: 0.9, shininess: 100 }),
        new THREE.MeshPhongMaterial({ color: 0x6CA5EA, transparent: true, opacity: 0.9, shininess: 100 }),
        new THREE.MeshPhongMaterial({ color: 0x4682B4, transparent: true, opacity: 0.9, shininess: 100 }),
        new THREE.MeshPhongMaterial({ color: 0x7EC8E3, transparent: true, opacity: 0.9, shininess: 100 })
    ];

    const geometry = new THREE.BoxGeometry(2, 2, 2);
    const cube = new THREE.Mesh(geometry, materials);
    
    const edges = new THREE.EdgesGeometry(geometry);
    const lineMaterial = new THREE.LineBasicMaterial({ color: 0x87CEEB, linewidth: 2 });
    const wireframe = new THREE.LineSegments(edges, lineMaterial);
    cube.add(wireframe);

    scene.add(cube);

    const ambientLight = new THREE.AmbientLight(0xffffff, 0.6);
    scene.add(ambientLight);

    const pointLight1 = new THREE.PointLight(0x87CEEB, 1, 100);
    pointLight1.position.set(5, 5, 5);
    scene.add(pointLight1);

    const pointLight2 = new THREE.PointLight(0x4169E1, 0.8, 100);
    pointLight2.position.set(-5, -5, 5);
    scene.add(pointLight2);

    camera.position.z = 5;

    let time = 0;
    let assembling = true;
    let rotating = false;
    let pulsing = false;

    const pieces = [];
    
    function createPieces() {
        const pieceGeometry = new THREE.BoxGeometry(2, 2, 2);
        for (let i = 0; i < 6; i++) {
            const pieceMesh = new THREE.Mesh(pieceGeometry, materials[i].clone());
            pieceMesh.material.transparent = true;
            pieceMesh.material.opacity = 0;
            
            const offset = 5;
            switch(i) {
                case 0: pieceMesh.position.set(offset, 0, 0); break;
                case 1: pieceMesh.position.set(-offset, 0, 0); break;
                case 2: pieceMesh.position.set(0, offset, 0); break;
                case 3: pieceMesh.position.set(0, -offset, 0); break;
                case 4: pieceMesh.position.set(0, 0, offset); break;
                case 5: pieceMesh.position.set(0, 0, -offset); break;
            }
            
            pieces.push(pieceMesh);
            scene.add(pieceMesh);
        }
        cube.visible = false;
    }

    createPieces();

    function animate() {
        requestAnimationFrame(animate);
        time += 0.016;

        if (assembling && time < 2) {
            pieces.forEach((piece) => {
                piece.material.opacity = Math.min(time / 0.5, 1);
                const progress = Math.min(time / 2, 1);
                const eased = 1 - Math.pow(1 - progress, 3);
                
                piece.position.lerp(new THREE.Vector3(0, 0, 0), eased);
                piece.rotation.x = (1 - eased) * Math.PI * 2;
                piece.rotation.y = (1 - eased) * Math.PI * 2;
            });
        } else if (assembling) {
            assembling = false;
            rotating = true;
            pieces.forEach(piece => scene.remove(piece));
            cube.visible = true;
        }

        if (rotating && !pulsing && time < 4) {
            cube.rotation.x = (time - 2) * Math.PI;
            cube.rotation.y = (time - 2) * Math.PI;
        } else if (rotating && !pulsing) {
            rotating = false;
            pulsing = true;
            cube.rotation.x = 0;
            cube.rotation.y = 0;
        }

        if (pulsing) {
            const pulse = Math.sin(time * 2) * 0.15 + 1;
            cube.scale.set(pulse, pulse, pulse);
            cube.rotation.x += 0.01;
            cube.rotation.y += 0.01;
            
            materials.forEach((mat, i) => {
                mat.opacity = 0.8 + Math.sin(time * 2 + i) * 0.1;
            });
        }

        renderer.render(scene, camera);
    }

    animate();

    window.addEventListener('resize', () => {
        camera.aspect = container.clientWidth / container.clientHeight;
        camera.updateProjectionMatrix();
        renderer.setSize(container.clientWidth, container.clientHeight);
    });
</script>
{% endraw %}