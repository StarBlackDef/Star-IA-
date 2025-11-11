# Star-IA-
Uma inteligência artificial para ajudar com tudo o que precisar
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Star IA - Geração Multimídia</title>
    <!-- Carrega o Tailwind CSS para um design responsivo e moderno -->
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        /* Novo tema escuro, fundo chumbo */
        body {
            font-family: 'Inter', sans-serif;
            background-color: #1C1C1C; /* Fundo chumbo escuro */
            color: #e5e5e5; /* Texto cinza claro */
            min-height: 100vh;
        }
        .container {
            max-width: 800px;
            margin: 0 auto;
            padding: 1rem;
        }
        .card {
            background-color: #262626; /* Cor de card/painel ligeiramente mais clara */
            border-radius: 12px;
            padding: 1.5rem;
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.2), 0 4px 6px -2px rgba(0, 0, 0, 0.1);
        }
        /* Cor de destaque principal: Índigo/Roxo */
        .btn-primary {
            background-color: #4f46e5; /* Índigo vibrante */
            color: white;
            padding: 0.75rem 1.5rem;
            border-radius: 8px;
            font-weight: 600;
            transition: background-color 0.3s;
        }
        .btn-primary:hover {
            background-color: #4338ca; /* Índigo um pouco mais escuro */
        }
        textarea, input[type="text"] {
            background-color: #1f1f1f; /* Fundo do input mais escuro */
            border: 1px solid #404040; /* Borda sutil */
            color: #e5e5e5;
            border-radius: 8px;
            padding: 0.75rem;
            transition: border-color 0.3s;
        }
        textarea:focus, input[type="text"]:focus {
            border-color: #4f46e5; /* Borda de foco Índigo */
            outline: none;
        }
        .result-container {
            min-height: 200px;
            max-height: 60vh;
            overflow-y: auto;
            white-space: pre-wrap;
            word-wrap: break-word;
            padding: 1rem;
            background-color: #1f1f1f;
            border-radius: 8px;
            border: 1px dashed #404040;
        }
        /* Estilização dos botões de estilo de imagem */
        .btn-style {
            background-color: #404040;
            color: #e5e5e5;
            padding: 0.5rem 1rem;
            border-radius: 9999px; /* Botão arredondado */
            font-size: 0.875rem;
            cursor: pointer;
            transition: background-color 0.3s, border-color 0.3s;
            border: 1px solid #404040;
        }
        .btn-style:hover {
            background-color: #525252;
        }
        .btn-style.selected {
            background-color: #4f46e5;
            border-color: #4f46e5;
            color: white;
        }
        /* Estilização do Toast para mensagens/erros */
        #toast {
            position: fixed;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            padding: 10px 20px;
            background-color: #333;
            color: white;
            border-radius: 6px;
            z-index: 1000;
            opacity: 0;
            transition: opacity 0.5s, transform 0.5s;
            pointer-events: none;
        }
        #toast.show {
            opacity: 1;
            transform: translateX(-50%) translateY(0);
        }
        .radio-mode:checked + label {
            background-color: #4f46e5;
            color: white;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
        }
    </style>
</head>
<body>

    <div class="container">
        <!-- Título com o ícone de estrela -->
        <h1 class="text-3xl font-bold text-center my-6 text-white flex items-center justify-center">
            <svg class="w-8 h-8 text-white mr-3" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118l-2.8-2.034c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
            </svg>
            Star IA
        </h1>
        <p class="text-center mb-6 text-sm text-gray-400">Geração multimídia: Defina o modo e insira seu prompt principal.</p>

        <!-- Seção de Entrada Unificada -->
        <div class="card mb-8">
            <h2 class="text-xl font-semibold mb-4 text-indigo-400">Modo de Geração</h2>

            <!-- Seletor de Modo -->
            <div class="flex space-x-2 mb-4 p-1 bg-gray-700 rounded-lg shadow-inner w-full sm:w-2/3 mx-auto">
                <input type="radio" id="modeText" name="generationMode" value="text" class="hidden radio-mode" checked onchange="toggleOptions()">
                <label for="modeText" class="flex-1 text-center py-2 px-4 text-sm font-medium rounded-md cursor-pointer transition duration-200 text-gray-300 hover:bg-gray-600">
                    Texto / Q&A
                </label>

                <input type="radio" id="modeImage" name="generationMode" value="image" class="hidden radio-mode" onchange="toggleOptions()">
                <label for="modeImage" class="flex-1 text-center py-2 px-4 text-sm font-medium rounded-md cursor-pointer transition duration-200 text-gray-300 hover:bg-gray-600">
                    Imagem (Foto)
                </label>
            </div>
            
            <h3 class="text-lg font-semibold mb-2 text-white text-center">Prompt Principal</h3>
            
            <textarea id="mainPrompt" class="w-full h-32 mb-4" placeholder="O que você gostaria que a Star IA gerasse ou respondesse?" rows="5"></textarea>
            
            <!-- Opções Condicionais -->
            <div id="optionsContainer">
                <!-- Opções de Texto (Padrão) -->
                <div id="textOptions" class="flex justify-center items-center mb-4">
                    <input type="checkbox" id="useSearch" class="h-4 w-4 text-indigo-600 border-gray-300 rounded focus:ring-indigo-500 mr-2 bg-gray-700 border-gray-600">
                    <label for="useSearch" class="text-sm text-gray-300">Usar Busca na Web (para fatos)</label>
                </div>
                
                <!-- Opções de Imagem (Inicialmente Ocultas) -->
                <div id="imageOptions" class="hidden mb-4">
                    <p class="text-sm font-semibold mb-2 text-gray-300 text-center">Ou escolha um estilo de arte (opcional):</p>
                    <div class="flex flex-wrap justify-center gap-2">
                        <!-- Estilos de Imagem -->
                        <button class="btn-style" onclick="selectStyle(this, 'Cinematográfico, Iluminação Volumétrica, 8K')">
                            Cinematográfico
                        </button>
                        <button class="btn-style" onclick="selectStyle(this, 'Pintura a Óleo Clássica')">
                            Pintura a Óleo
                        </button>
                        <button class="btn-style" onclick="selectStyle(this, 'Pixel Art, 16 bits')">
                            Pixel Art
                        </button>
                        <button class="btn-style" onclick="selectStyle(this, 'Arte Conceitual, Ambiente Sci-Fi')">
                            Sci-Fi Conceitual
                        </button>
                    </div>
                </div>
            </div>
            
            <button class="btn-primary w-full" onclick="generateContent()" id="generateBtn">
                Gerar Conteúdo
            </button>
        </div>

        <!-- Resultados -->
        <div class="card">
            <h2 class="text-xl font-semibold mb-4 text-white">Resultados</h2>
            <div id="results" class="result-container">
                <p class="text-gray-500">O conteúdo gerado aparecerá aqui...</p>
            </div>
            <div id="loading" class="text-center my-4 hidden">
                <svg class="animate-spin h-6 w-6 text-indigo-400 inline-block mr-2" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
                    <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                    <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
                </svg>
                <span id="loadingMessage">Processando...</span>
            </div>
        </div>
        
        <!-- Observação sobre Vídeo -->
        <div class="mt-6 p-4 bg-yellow-900 bg-opacity-50 border border-yellow-700 rounded-lg text-sm text-yellow-300">
            <strong>Nota sobre Vídeo:</strong> A criação de vídeos requer modelos de IA extremamente complexos e grande capacidade de processamento. Esta funcionalidade não está disponível nesta demonstração em um único arquivo, mas sistemas de IA dedicados já podem gerar vídeos curtos a partir de texto.
        </div>

    </div>

    <!-- Toast de Mensagens -->
    <div id="toast"></div>

    <script>
        // Variáveis globais para configuração da API (mantidas vazias conforme instrução)
        const apiKey = ""; 
        const TEXT_MODEL = "gemini-2.5-flash-preview-09-2025";
        const IMAGE_MODEL = "imagen-4.0-generate-001";

        const resultsDiv = document.getElementById('results');
        const loadingDiv = document.getElementById('loading');
        const loadingMessageSpan = document.getElementById('loadingMessage');
        const generateBtn = document.getElementById('generateBtn');
        const mainPromptTextarea = document.getElementById('mainPrompt');
        const textOptionsDiv = document.getElementById('textOptions');
        const imageOptionsDiv = document.getElementById('imageOptions');
        const useSearchCheckbox = document.getElementById('useSearch');
        
        // Estado global para o estilo de imagem selecionado
        let selectedImageStyle = '';
        
        /**
         * Lida com a seleção dos botões de estilo de imagem.
         */
        function selectStyle(button, styleText) {
            const buttons = imageOptionsDiv.querySelectorAll('.btn-style');
            
            // Remove a seleção de todos os botões
            buttons.forEach(btn => btn.classList.remove('selected'));
            
            if (selectedImageStyle === styleText) {
                // Se o estilo já estiver selecionado, deseleciona
                selectedImageStyle = '';
            } else {
                // Seleciona o novo estilo
                button.classList.add('selected');
                selectedImageStyle = styleText;
            }
        }

        /**
         * Alterna a visibilidade das opções e altera o placeholder do prompt principal.
         */
        function toggleOptions() {
            const selectedMode = document.querySelector('input[name="generationMode"]:checked').value;
            
            // Redefine o estilo selecionado ao trocar de modo
            selectedImageStyle = '';
            imageOptionsDiv.querySelectorAll('.btn-style').forEach(btn => btn.classList.remove('selected'));


            if (selectedMode === 'text') {
                textOptionsDiv.classList.remove('hidden');
                imageOptionsDiv.classList.add('hidden');
                mainPromptTextarea.placeholder = "O que você gostaria que a Star IA gerasse ou respondesse?";
            } else {
                textOptionsDiv.classList.add('hidden');
                imageOptionsDiv.classList.remove('hidden');
                mainPromptTextarea.placeholder = "Descreva a foto (imagem) que você quer criar (Ex: Um leão de óculos escuros na lua).";
            }
        }
        
        // Inicializa a visibilidade na carga
        toggleOptions();


        /**
         * Função principal para gerar conteúdo, decidindo o modo.
         */
        function generateContent() {
            const selectedMode = document.querySelector('input[name="generationMode"]:checked').value;
            
            if (selectedMode === 'text') {
                generateText();
            } else if (selectedMode === 'image') {
                generateImage();
            }
        }

        /**
         * Exibe uma mensagem de notificação (Toast) em vez de usar alert().
         * @param {string} message A mensagem a ser exibida.
         * @param {number} duration Duração em milissegundos.
         */
        function showToast(message, duration = 3000) {
            const toast = document.getElementById('toast');
            toast.textContent = message;
            toast.classList.add('show');
            setTimeout(() => {
                toast.classList.remove('show');
            }, duration);
        }

        /**
         * Wrapper de fetch com retry e backoff exponencial.
         * @param {string} url URL para a requisição.
         * @param {object} options Opções de fetch (method, headers, body).
         * @param {number} maxRetries Número máximo de tentativas.
         * @param {number} delay Tempo de espera inicial (em ms).
         * @returns {Promise<Response>} A resposta da requisição.
         */
        async function exponentialBackoffFetch(url, options, maxRetries = 5, delay = 1000) {
            for (let i = 0; i < maxRetries; i++) {
                try {
                    const response = await fetch(url, options);
                    if (response.status !== 429) { // 429: Too Many Requests
                        return response;
                    }
                    if (i === maxRetries - 1) {
                        throw new Error("Limite de taxa excedido após múltiplas tentativas.");
                    }
                    console.log(`Tentativa ${i + 1} falhou com 429. Aguardando ${delay}ms...`);
                } catch (error) {
                    if (i === maxRetries - 1) throw error;
                    console.log(`Tentativa ${i + 1} falhou com erro. Aguardando ${delay}ms...`, error);
                }
                await new Promise(resolve => setTimeout(resolve, delay));
                delay *= 2; // Dobra o tempo de espera
            }
        }

        /**
         * Converte uma string de prompt em um prompt mais descritivo para geração de imagem.
         * @param {string} prompt O prompt original em Português.
         * @param {string} style O estilo pré-selecionado (ou vazio).
         * @returns {string} O prompt traduzido para o Inglês e aprimorado.
         */
        async function enhanceAndTranslatePrompt(prompt, style) {
            const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/${TEXT_MODEL}:generateContent?key=${apiKey}`;
            
            const systemPrompt = `Você é um tradutor e aprimorador de prompts de imagem.
            1. O usuário forneceu um prompt em Português: "${prompt}".
            2. O usuário também selecionou o estilo adicional: "${style}".
            3. Combine o prompt do usuário com o estilo (se houver) e adicione melhorias técnicas de imagem (como 'photorealistic', '8k', 'high detail').
            4. Traduza o resultado final (prompt aprimorado) para o INGLÊS.
            5. O resultado deve ser APENAS o prompt aprimorado em INGLÊS. Não inclua nenhuma outra frase ou formatação.`;

            const payload = {
                contents: [{ parts: [{ text: prompt }] }],
                systemInstruction: { parts: [{ text: systemPrompt }] },
            };

            try {
                const response = await exponentialBackoffFetch(apiUrl, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });

                if (!response.ok) {
                    throw new Error(`Erro HTTP: ${response.status}`);
                }

                const result = await response.json();
                const translatedPrompt = result.candidates?.[0]?.content?.parts?.[0]?.text?.trim();

                if (translatedPrompt) {
                    console.log("Prompt aprimorado (EN):", translatedPrompt);
                    return translatedPrompt;
                }
            } catch (error) {
                console.error("Erro ao traduzir/aprimorar o prompt de imagem:", error);
                // Retorna o prompt original + estilo como fallback
                return prompt + (style ? `, ${style}` : ''); 
            }
            return prompt + (style ? `, ${style}` : ''); // Fallback final
        }

        /**
         * Lida com a geração de Imagem (Foto) usando o modelo Imagen.
         */
        async function generateImage() {
            const prompt = mainPromptTextarea.value.trim();
            if (!prompt) {
                showToast("Por favor, insira um prompt para gerar a foto.");
                return;
            }

            // Desabilita botões e exibe loading
            generateBtn.disabled = true;
            loadingMessageSpan.textContent = "Aprimorando prompt e gerando foto...";
            loadingDiv.classList.remove('hidden');
            resultsDiv.innerHTML = '';
            
            try {
                // 1. Aprimorar e traduzir o prompt para inglês
                const styleToApply = selectedImageStyle;
                const enhancedPrompt = await enhanceAndTranslatePrompt(prompt, styleToApply);

                // 2. Chamar a API de Geração de Imagem
                const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/${IMAGE_MODEL}:predict?key=${apiKey}`;
                
                const payload = {
                    instances: { prompt: enhancedPrompt },
                    parameters: { "sampleCount": 1 }
                };

                const response = await exponentialBackoffFetch(apiUrl, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });
                
                if (!response.ok) {
                    throw new Error(`Erro de rede ou API: ${response.status}`);
                }
                
                const result = await response.json();
                
                const base64Data = result.predictions && result.predictions.length > 0
                    ? result.predictions[0].bytesBase64Encoded
                    : null;
                
                if (base64Data) {
                    const imageUrl = `data:image/png;base64,${base64Data}`;
                    resultsDiv.innerHTML = `
                        <div class="flex flex-col items-center">
                            <h3 class="text-lg font-bold mb-2 text-indigo-400">Foto Gerada</h3>
                            <img src="${imageUrl}" alt="${prompt}" class="max-w-full h-auto rounded-lg shadow-lg" style="max-height: 400px; object-fit: contain;">
                            <p class="mt-4 text-sm text-gray-400 italic">Prompt Original: "${prompt}"</p>
                            ${styleToApply ? `<p class="text-xs text-gray-500 italic">Estilo Aplicado: ${styleToApply}</p>` : ''}
                        </div>
                    `;
                } else {
                    showToast("Erro: A IA não conseguiu gerar a imagem com este prompt.");
                    resultsDiv.innerHTML = `<p class="text-red-400">Falha ao gerar a imagem. Tente um prompt diferente.</p>`;
                }

            } catch (error) {
                console.error("Erro na geração de imagem:", error);
                showToast(`Ocorreu um erro: ${error.message}`);
                resultsDiv.innerHTML = `<p class="text-red-400">Erro durante o processamento da imagem: ${error.message}</p>`;
            } finally {
                generateBtn.disabled = false;
                loadingDiv.classList.add('hidden');
            }
        }
        
        /**
         * Lida com a geração de Texto e Q&A usando o modelo Gemini.
         */
        async function generateText() {
            const prompt = mainPromptTextarea.value.trim();
            const useSearch = useSearchCheckbox.checked;

            if (!prompt) {
                showToast("Por favor, insira um prompt para gerar o texto ou fazer a pergunta.");
                return;
            }

            // Desabilita botões e exibe loading
            generateBtn.disabled = true;
            loadingMessageSpan.textContent = useSearch ? "Buscando na web e gerando resposta..." : "Gerando conteúdo de texto...";
            loadingDiv.classList.remove('hidden');
            resultsDiv.innerHTML = '';

            try {
                const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/${TEXT_MODEL}:generateContent?key=${apiKey}`;
                
                const systemPrompt = "Você é um assistente de IA prestativo e criativo. Responda em Português. Seja conciso e direto. Se estiver usando a busca, use as informações mais atuais para responder à pergunta ou completar a tarefa.";

                const payload = {
                    contents: [{ parts: [{ text: prompt }] }],
                    systemInstruction: { parts: [{ text: systemPrompt }] },
                };

                // Adiciona a ferramenta de busca se o checkbox estiver marcado
                if (useSearch) {
                    payload.tools = [{ "google_search": {} }];
                }

                const response = await exponentialBackoffFetch(apiUrl, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });

                if (!response.ok) {
                    throw new Error(`Erro de rede ou API: ${response.status}`);
                }

                const result = await response.json();
                const candidate = result.candidates?.[0];

                if (candidate && candidate.content?.parts?.[0]?.text) {
                    const generatedText = candidate.content.parts[0].text;
                    let sourcesHtml = '';

                    // Extrai as fontes de aterramento (grounding) se a busca foi usada
                    const groundingMetadata = candidate.groundingMetadata;
                    if (groundingMetadata && groundingMetadata.groundingAttributions) {
                        const sources = groundingMetadata.groundingAttributions
                            .map(attribution => ({
                                uri: attribution.web?.uri,
                                title: attribution.web?.title,
                            }))
                            .filter(source => source.uri && source.title);

                        if (sources.length > 0) {
                            sourcesHtml = '<p class="text-sm mt-4 font-semibold text-indigo-400">Fontes:</p><ul class="list-disc list-inside text-xs text-gray-500 mt-1">';
                            sources.forEach((source, index) => {
                                sourcesHtml += `<li><a href="${source.uri}" target="_blank" class="hover:underline text-blue-400">${source.title}</a></li>`;
                            });
                            sourcesHtml += '</ul>';
                        }
                    }

                    resultsDiv.innerHTML = `<h3 class="text-lg font-bold mb-2 text-indigo-400">Texto/Resposta Gerada</h3><div class="whitespace-pre-wrap">${generatedText}</div>${sourcesHtml}`;
                    resultsDiv.scrollTop = resultsDiv.scrollHeight; // Rola para o final do conteúdo
                } else {
                    showToast("Erro: A IA não conseguiu gerar uma resposta com este prompt.");
                    resultsDiv.innerHTML = `<p class="text-red-400">Falha ao gerar o texto. A resposta da IA estava vazia.</p>`;
                }

            } catch (error) {
                console.error("Erro na geração de texto/Q&A:", error);
                showToast(`Ocorreu um erro: ${error.message}`);
                resultsDiv.innerHTML = `<p class="text-red-400">Erro durante o processamento do texto: ${error.message}</p>`;
            } finally {
                generateBtn.disabled = false;
                loadingDiv.classList.add('hidden');
            }
        }
    </script>
</body>
</html>


