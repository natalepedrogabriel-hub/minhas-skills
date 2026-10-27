---
name: "ranqueador-curriculos"
description: "Use quando o usuário pedir para triar, avaliar ou ranquear currículos para uma vaga, com critérios e pesos escolhidos pela empresa."
---

# Ranqueador de currículos

Ranqueia candidatos por aderência a uma vaga. A IA apenas ordena e justifica: não contata candidatos, não agenda entrevistas e não decide contratação. A decisão é sempre da empresa.

## 1. Coletar a vaga

Pergunte só o que faltar, numa única mensagem:
- Cargo
- Pré-requisitos
- Faixa salarial (opcional)
- Modelo de trabalho: presencial, híbrido ou remoto, e cidade

## 2. Definir critérios e pesos (a empresa escolhe)

Ofereça a lista padrão e deixe a empresa ligar, desligar, ajustar pesos ou criar critérios próprios:

| Critério | O que avalia | Peso padrão |
| --- | --- | --- |
| Pré-requisitos obrigatórios | Atende ou não aos itens eliminatórios | Filtro |
| Experiência relevante | Tempo e similaridade com cargos anteriores | 35% |
| Habilidades técnicas | Correspondência com as competências pedidas | 30% |
| Formação e certificações | Nível e área de formação | 15% |
| Localização e modelo de trabalho | Compatibilidade com o modelo da vaga | 10% |
| Pretensão salarial | Compatibilidade com a faixa, quando informada | 10% |

Regras:
- Os pesos dos critérios pontuados devem somar exatamente 100%. Se não somarem, mostre a soma e peça ajuste antes de seguir.
- Critério marcado como obrigatório vira filtro eliminatório (sem peso).
- Recuse critérios baseados em idade, gênero, foto, estado civil, religião, raça, deficiência ou endereço exato, explicando em uma frase que eles geram discriminação.
- Se o usuário disser "usa o padrão", siga com a lista padrão sem perguntar mais.

## 3. Coletar os currículos

- Currículos anexados (PDF ou Word): leia cada arquivo por completo.
- Pasta no Google Drive: use o conector do Drive para listar a pasta indicada e ler cada currículo. Se o conector não estiver disponível, peça para anexar os arquivos.
- Se um arquivo vier ilegível ou quase vazio (ex.: PDF escaneado sem texto), marque como "leitura incompleta" e liste no final em vez de pontuar.

## 4. Extrair dados de cada candidato

Para cada currículo, registre: nome, contato, cidade, formação, experiências (cargo, empresa, período), habilidades, idiomas e pretensão salarial.

Nunca extraia nem use idade, gênero, estado civil, religião, foto ou endereço exato.

## 5. Avaliar

Para cada candidato e cada critério:
- Nota inteira de 0 a 10.
- Justificativa de no máximo 2 frases, em português simples, citando o que está no currículo.
- Se a informação não estiver no currículo: nota 0 e "não informado". Não suponha.
- Para critérios obrigatórios: "atende" ou "não atende", com o motivo.

Avalie todos os candidatos com o mesmo rigor e pelos mesmos critérios.

## 6. Calcular a nota final

Faça a conta com código (Python), não de cabeça, para o resultado ser exato e reproduzível:

- Se não atende a algum obrigatório: eliminado (sem nota final).
- Senão: nota final = soma de (nota do critério × peso em %) ÷ 10, de 0 a 100.
- Ordene do maior para o menor; em empate, desempate pela maior nota no critério de maior peso.

## 7. Perguntas de entrevista para o top 3

Para cada um dos 3 primeiros colocados (só candidatos não eliminados; se houver menos de 3, faça para os que houver), gere 5 perguntas personalizadas a partir do currículo e das notas:

1. Duas sobre os critérios com nota mais baixa, para investigar as lacunas.
2. Uma para confirmar algo marcado como "não informado" ou pouco claro no currículo. Se não houver, troque por mais uma sobre lacuna.
3. Uma pedindo um exemplo concreto da experiência mais relevante para a vaga, no formato situação, tarefa, ação e resultado.
4. Uma situacional, sobre um problema típico do dia a dia do cargo.

Para cada pergunta, inclua em uma frase cada:
- O que ela investiga.
- Sinal de boa resposta.

Regras:
- Escreva como o recrutador falaria numa conversa, sem jargão.
- Cite fatos do currículo do candidato (empresa, cargo, ferramenta), para a pergunta não ser genérica.
- Nunca pergunte sobre idade, filhos, gravidez, planos de família, estado civil, religião, saúde, deficiência, orientação sexual, raça, origem ou política.
- As perguntas são um roteiro para a empresa usar; a skill não envia nada ao candidato nem agenda entrevista.

## 8. Entregar

1. No chat, uma frase com o resultado principal (ex.: quantos candidatos, quantos eliminados, quem lidera) e uma tabela com o top 5: posição, nome, nota final, ponto forte, ponto fraco.
2. Uma planilha completa (artefato de planilha, se disponível; senão arquivo .xlsx) com quatro abas:
   - Ranking: posição, nome, contato, nota final, nota por critério.
   - Justificativas: candidato, critério, nota, justificativa.
   - Perguntas de entrevista: candidato, pergunta, o que investiga, sinal de boa resposta.
   - Eliminados e pendentes: nome, motivo (obrigatório não atendido ou leitura incompleta).
3. Uma linha final lembrando que a decisão e o contato com os candidatos ficam com a empresa.

## 9. Treinamento do contratado (opcional)

Se o usuário informar que contratou alguém do ranking, ofereça gerar uma trilha de onboarding em documento:
- Objetivos da primeira semana e do primeiro mês.
- Tópicos a estudar e tarefas práticas para o cargo.
- Pontos de reforço nos critérios em que o contratado teve as notas mais baixas.

## Privacidade (LGPD)

- Não salve dados de candidatos na memória.
- Não compartilhe dados de um processo seletivo em outro.
- Se o usuário pedir algo que exija contatar, agendar ou decidir por candidatos, explique que esta skill só ranqueia.
