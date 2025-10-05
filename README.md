<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quiz Bioquímica - 20 Perguntas</title>
    <style>
        body {
            font-family: 'Segoe UI', Arial, sans-serif;
            background: #f6f8fa;
            color: #222;
            margin: 0;
            padding: 0;
        }
        .container {
            max-width: 700px;
            margin: auto;
            background: #fff;
            box-shadow: 0 2px 14px rgba(0,0,0,0.08);
            border-radius: 10px;
            padding: 30px 24px 24px 24px;
            margin-top: 36px;
        }
        h1 {
            text-align: center;
            color: #117a8b;
        }
        .start-btn, .nav-btn, .finish-btn, .restart-btn {
            background: #117a8b;
            color: #fff;
            border: none;
            padding: 12px 24px;
            border-radius: 7px;
            font-size: 1.1rem;
            margin: 16px auto;
            display: block;
            cursor: pointer;
            box-shadow: 0 2px 4px rgba(0,0,0,0.06);
            transition: background 0.2s;
        }
        .start-btn:hover, .nav-btn:hover, .finish-btn:hover, .restart-btn:hover { background: #0e606b; }
        .question-count {
            text-align: right;
            font-size: 0.98rem;
            color: #555;
            margin-bottom: 10px;
        }
        .question-text {
            font-size: 1.18rem;
            margin-bottom: 18px;
            color: #1b4f72;
        }
        .options label {
            display: block;
            background: #f4f6f9;
            padding: 12px 14px;
            margin-bottom: 10px;
            border-radius: 6px;
            cursor: pointer;
            transition: background 0.2s;
        }
        .options input[type=radio] {
            margin-right: 14px;
        }
        .options label.selected {
            background: #e9f7ef;
            border-left: 4px solid #117a8b;
        }
        .feedback {
            margin-top: 14px;
            font-weight: bold;
            border-radius: 6px;
            padding: 12px;
            display: none;
        }
        .correct { background: #e9f7ef; color: #155724; border: 1px solid #c3e6cb; }
        .incorrect { background: #fdecea; color: #7a1f1f; border: 1px solid #f5c6cb; }
        .note { color: #555; font-size: 0.96rem; text-align: center; margin-bottom: 22px;}
        .result {
            text-align: center;
            margin-top: 40px;
        }
        .score {
            font-size: 1.35rem;
            font-weight: bold;
            margin-bottom: 16px;
            color: #117a8b;
        }
        @media (max-width: 600px) {
            .container { padding: 12px 6px; }
            h1 { font-size: 1.2rem; }
        }
    </style>
</head>
<body>
    <div class="container" id="main-container">
        <h1>Quiz de Bioquímica</h1>
        <div class="note">Teste seus conhecimentos em bioquímica! 20 perguntas didáticas, com feedback explicativo após cada resposta.</div>
        <button class="start-btn" id="start-btn">Iniciar Quiz</button>
    </div>

    <script>
        // Perguntas do quiz
        const questions = [
            {
                text: "A bioquímica estuda principalmente:",
                options: [
                    {text: "A evolução das espécies", value: "a"},
                    {text: "As reações químicas nos organismos vivos", value: "b"},
                    {text: "A anatomia dos órgãos", value: "c"}
                ],
                correct: "b",
                explanation: "✅ Correto! Bioquímica = reações químicas dentro das células e organismos."
            },
            {
                text: "Qual propriedade da água explica a formação de pontes de hidrogênio?",
                options: [
                    {text: "Sua apolaridade", value: "a"},
                    {text: "Sua polaridade", value: "b"},
                    {text: "Sua alta massa molecular", value: "c"}
                ],
                correct: "b",
                explanation: "✅ Correto! A água é polar, com polos + e -, formando pontes de H entre moléculas."
            },
            {
                text: "O que é um sistema tampão?",
                options: [
                    {text: "Substância que aumenta sempre o pH", value: "a"},
                    {text: "Sistema que resiste a variações de pH", value: "b"},
                    {text: "Um tipo de enzima digestiva", value: "c"}
                ],
                correct: "b",
                explanation: "✅ Correto! Tampões mantêm o pH estável quando ácidos ou bases são adicionados."
            },
            {
                text: "Qual é o principal tampão do sangue?",
                options: [
                    {text: "Fosfato", value: "a"},
                    {text: "Hemoglobina", value: "b"},
                    {text: "Bicarbonato", value: "c"}
                ],
                correct: "c",
                explanation: "✅ Correto! Sistema bicarbonato (H2CO3 / HCO3-) é o principal tampão sanguíneo."
            },
            {
                text: "Na acidose respiratória há:",
                options: [
                    {text: "Aumento de CO2 e queda do pH", value: "a"},
                    {text: "Perda de bicarbonato pelo rim", value: "b"},
                    {text: "Aumento do pH", value: "c"}
                ],
                correct: "a",
                explanation: "✅ Correto! Retenção de CO2 forma mais H2CO3 → mais H+ → pH baixa."
            },
            {
                text: "Aminoácidos essenciais são aqueles que:",
                options: [
                    {text: "O corpo sintetiza em quantidade suficiente", value: "a"},
                    {text: "Devem ser obtidos pela alimentação", value: "b"},
                    {text: "Não possuem grupo amina", value: "c"}
                ],
                correct: "b",
                explanation: "✅ Correto! Essenciais não são produzidos pelo organismo e vêm da dieta."
            },
            {
                text: "A ligação peptídica une:",
                options: [
                    {text: "Dois ácidos graxos", value: "a"},
                    {text: "Dois nucleotídeos", value: "b"},
                    {text: "Dois aminoácidos", value: "c"}
                ],
                correct: "c",
                explanation: "✅ Correto! Ligação peptídica entre grupo carboxila de um AA e amina do outro forma peptídeos/proteínas."
            },
            {
                text: "Qual estrutura proteica é descrita como sequência linear de aminoácidos?",
                options: [
                    {text: "Estrutura primária", value: "a"},
                    {text: "Estrutura secundária", value: "b"},
                    {text: "Estrutura terciária", value: "c"}
                ],
                correct: "a",
                explanation: "✅ Correto! Primária = sequência de AAs ligada por ligações covalentes (peptídicas)."
            },
            {
                text: "A estrutura secundária de proteínas envolve principalmente:",
                options: [
                    {text: "Ligações de hidrogênio formando hélices ou folhas", value: "a"},
                    {text: "Ligações peptídicas apenas", value: "b"},
                    {text: "Ligações dissulfeto só", value: "c"}
                ],
                correct: "a",
                explanation: "✅ Correto! Pontes de H entre grupos da cadeia formam alfa-hélice e folhas-beta."
            },
            {
                text: "Desnaturação proteica geralmente causa:",
                options: [
                    {text: "Ganho de função", value: "a"},
                    {text: "Perda da estrutura tridimensional e função", value: "b"},
                    {text: "Transformação em carboidrato", value: "c"}
                ],
                correct: "b",
                explanation: "✅ Correto! Alterar forma 3D destrói o sítio ativo → perda de função."
            },
            {
                text: "Enzimas são melhor descritas como:",
                options: [
                    {text: "Catalisadores proteicos que aceleram reações", value: "a"},
                    {text: "Substratos das reações", value: "b"},
                    {text: "Lipídios da membrana", value: "c"}
                ],
                correct: "a",
                explanation: "✅ Correto! Enzimas aceleram reações e não se consomem no processo."
            },
            {
                text: "Em inibição competitiva, o que acontece quando se aumenta a concentração de substrato?",
                options: [
                    {text: "A inibição é superada e velocidade aumenta", value: "a"},
                    {text: "A inibição fica mais forte", value: "b"},
                    {text: "A enzima é degradada", value: "c"}
                ],
                correct: "a",
                explanation: "✅ Correto! Competitivo compete pelo sítio ativo; mais substrato desloca o inibidor."
            },
            {
                text: "Em inibição não competitiva, aumentar substrato:",
                options: [
                    {text: "Restaura totalmente a atividade enzimática", value: "a"},
                    {text: "Não altera a inibição, pois o inibidor age em outro sítio", value: "b"},
                    {text: "Transforma o inibidor em substrato", value: "c"}
                ],
                correct: "b",
                explanation: "✅ Correto! Não competitivo muda a forma da enzima; substrato extra não resolve."
            },
            {
                text: "Qual é a fórmula geral dos carboidratos?",
                options: [
                    {text: "Cn(H2O)n", value: "a"},
                    {text: "CnH2nOn (ou (CH2O)n)", value: "b"},
                    {text: "CnHnOn", value: "c"}
                ],
                correct: "b",
                explanation: "✅ Correto! Fórmula geral: (CH2O)n — relação 1:2:1 entre C:H:O."
            },
            {
                text: "Hemoglobina glicada (HbA1c) reflete:",
                options: [
                    {text: "Controle médio da glicose nos últimos 3 meses", value: "a"},
                    {text: "Níveis instantâneos de glicose", value: "b"},
                    {text: "Quantidade de hemácias no sangue", value: "c"}
                ],
                correct: "a",
                explanation: "✅ Correto! HbA1c indica exposição média à glicose ~3 meses."
            },
            {
                text: "Lipídeos são solúveis em água?",
                options: [
                    {text: "Sim, altamente solúveis", value: "a"},
                    {text: "Não, são insolúveis em água", value: "b"},
                    {text: "Apenas os ácidos graxos são solúveis", value: "c"}
                ],
                correct: "b",
                explanation: "✅ Correto! Lipídeos são hidrofóbicos e insolúveis em água."
            },
            {
                text: "Triacilgliceróis servem principalmente para:",
                options: [
                    {text: "Armazenamento de energia", value: "a"},
                    {text: "Catalisar reações", value: "b"},
                    {text: "Transmissão de sinais nervosos", value: "c"}
                ],
                correct: "a",
                explanation: "✅ Correto! Triacilgliceróis em adipócitos armazenam energia como gordura."
            },
            {
                text: "Vitaminas lipossolúveis (ex: D3, A) estão relacionadas a:",
                options: [
                    {text: "Funções como hormônios, visão e regulação mineral", value: "a"},
                    {text: "Atuar só como carboidratos", value: "b"},
                    {text: "Ser solúveis em água", value: "c"}
                ],
                correct: "a",
                explanation: "✅ Correto! Vitamina D3 regula cálcio; A está ligada à visão, entre outras funções."
            },
            {
                text: "Qual fator NÃO altera a atividade enzimática?",
                options: [
                    {text: "pH", value: "a"},
                    {text: "Temperatura", value: "b"},
                    {text: "Cor do tubo de ensaio", value: "c"}
                ],
                correct: "c",
                explanation: "✅ Correto! Cor do tubo não altera atividade; pH e temperatura sim."
            },
            {
                text: "O modelo \"chave-fechadura\" descreve:",
                options: [
                    {text: "Ajuste perfeito entre enzima e substrato", value: "a"},
                    {text: "Modelo de membrana celular", value: "b"},
                    {text: "Estrutura do DNA", value: "c"}
                ],
                correct: "a",
                explanation: "✅ Correto! Chave-fechadura = encaixe específico entre sítio ativo e substrato."
            }
        ];

        // Estado do quiz
        let current = 0;
        let userAnswers = [];
        let feedbackStates = [];
        let score = 0;

        const container = document.getElementById('main-container');
        const startBtn = document.getElementById('start-btn');

        startBtn.onclick = () => { startQuiz(); };

        function startQuiz() {
            current = 0;
            userAnswers = Array(questions.length).fill(null);
            feedbackStates = Array(questions.length).fill(false);
            score = 0;
            showQuestion();
        }

        function showQuestion() {
            const q = questions[current];
            let html = `
                <div class="question-count">Pergunta ${current+1} de ${questions.length}</div>
                <div class="question-text">${q.text}</div>
                <form id="question-form">
                    <div class="options">
                        ${q.options.map((opt, i) => `
                            <label class="${userAnswers[current] === opt.value ? 'selected' : ''}">
                                <input type="radio" name="option" value="${opt.value}" ${userAnswers[current] === opt.value ? 'checked' : ''}>
                                ${opt.text}
                            </label>
                        `).join('')}
                    </div>
                    ${!feedbackStates[current] ? `<button type="button" class="nav-btn" id="check-btn">Verificar Resposta</button>` : ''}
                </form>
                <div class="feedback" id="feedback"></div>
                <div style="margin-top:18px;">
                    ${current > 0 ? '<button class="nav-btn" id="prev-btn">&larr; Anterior</button>' : ''}
                    ${current < questions.length-1 ? `<button class="nav-btn" id="next-btn" style="display:${feedbackStates[current] ? 'inline-block' : 'none'};">Próxima &rarr;</button>` : ''}
                    ${current === questions.length-1 && feedbackStates[current] ? '<button class="finish-btn" id="finish-btn">Ver Resultado</button>' : ''}
                </div>
            `;
            container.innerHTML = html;

            if (!feedbackStates[current]) {
                document.getElementById('check-btn').onclick = () => checkAnswer();
            }
            if (current > 0) document.getElementById('prev-btn').onclick = () => prevQuestion();
            if (current < questions.length-1) document.getElementById('next-btn').onclick = () => nextQuestion();
            if (current === questions.length-1 && feedbackStates[current]) document.getElementById('finish-btn').onclick = () => showResult();

            // Se já respondeu, mostra feedback
            if (feedbackStates[current]) showFeedback();
        }

        function checkAnswer() {
            const radios = document.getElementsByName('option');
            let selected = null;
            for (const r of radios) {
                if (r.checked) selected = r.value;
            }
            const feedback = document.getElementById('feedback');
            if (!selected) {
                feedback.textContent = "Por favor, selecione uma opção!";
                feedback.className = "feedback incorrect";
                feedback.style.display = "block";
                return;
            }
            userAnswers[current] = selected;
            feedbackStates[current] = true;
            if (!feedback.dataset.scored) {
                if (selected === questions[current].correct) score++;
                feedback.dataset.scored = "1";
            }
            showQuestion(); // Re-renderiza a pergunta, removendo botão de verificar e mostrando botão próxima
        }

        function showFeedback() {
            const feedback = document.getElementById('feedback');
            const q = questions[current];
            if (userAnswers[current] === q.correct) {
                feedback.innerHTML = q.explanation;
                feedback.className = "feedback correct";
            } else {
                let wrongText = q.explanation.replace('✅ Correto! ', '');
                feedback.innerHTML = `❌ Incorreto. ${wrongText}`;
                feedback.className = "feedback incorrect";
            }
            feedback.style.display = "block";
        }

        function nextQuestion() {
            current++;
            showQuestion();
        }
        function prevQuestion() {
            current--;
            showQuestion();
        }

        function showResult() {
            let html = `
                <div class="result">
                    <div class="score">Você acertou ${score} de ${questions.length} perguntas.</div>
                    <div style="margin:24px 0">
                        <button class="restart-btn" onclick="window.location.reload()">Refazer Quiz</button>
                    </div>
                    <div>
                        <h3>Gabarito:</h3>
                        <ul style="text-align:left;">
                            ${questions.map((q, i) => {
                                let user = userAnswers[i];
                                let isCorrect = user === q.correct;
                                let letter = q.options.find(opt => opt.value === q.correct).text;
                                return `<li>
                                        <strong>P${i+1}:</strong> <span style="color:${isCorrect?'#117a8b':'#7a1f1f'}">
                                            ${isCorrect ? "✔️" : "❌"}
                                        </span>
                                        <span>${q.text}<br>
                                        <em>Resposta correta: ${letter}</em>
                                        <br>
                                        <span style="font-size:0.97em">${q.explanation.replace('✅ Correto! ','')}</span>
                                        </span>
                                    </li>`;
                            }).join('')}
                        </ul>
                    </div>
                </div>
            `;
            container.innerHTML = html;
        }
    </script>
</body>
</html>
