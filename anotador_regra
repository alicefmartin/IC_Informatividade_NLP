import re
import pandas as pd

def limpar(texto):
    return re.sub(r"[^\w\sáéíóúãõç]", "", texto.lower()).strip()
def resposta_minima_completa(pergunta, resposta):
    resposta = resposta.strip().lower()
    pergunta = pergunta.lower()

    if resposta not in ["sim", "não"]:
        return False

    if " e " in pergunta or " ou " in pergunta:
        return False

    return True
def extrair_verbo_principal(pergunta):
    pergunta = limpar(pergunta)
    palavras = pergunta.split()

    # heurística simples: primeiro verbo flexionado comum
    for p in palavras:
        if p.endswith(("a","e","am","em","ou","eu","ia","ava","aram","eram","iram")):
            return p
    return None
def extrair_entidades(pergunta):
    texto = limpar(pergunta)

    # corta após o verbo para evitar ruído
    texto = re.split(
        r"\bfoi|foram|fala|falam|chegou|chegaram|participou|participaram|entregou|entregaram\b",
        texto
    )[0]

    partes = [p.strip() for p in texto.split(" e ")]

    stopwords = {
        "o","a","os","as","um","uma","do","da","de","no","na",
        "para","ao","à","dos","das"
    }

    entidades = []
    for p in partes:
        tokens = [t for t in p.split() if t not in stopwords]
        if tokens:
            entidades.append(tokens[-1])  # núcleo do SN

    return entidades
def classificar_informatividade(pergunta, resposta):
    pergunta_norm = limpar(pergunta)
    resposta_norm = limpar(resposta)

    #REGRA 0: resposta mínima ("sim" / "não") ---
    if resposta_minima_completa(pergunta_norm, resposta_norm):
        return "completa"

    #REGRA 1: resposta elíptica afirmativa ("sim, fala") ---
    verbo = extrair_verbo_principal(pergunta)
    if verbo:
        if resposta_norm.startswith(("sim","claro","com certeza","óbvio","aham")) and verbo in resposta_norm:
            return "completa"

    #REGRA 2: extrai entidades ---
    entidades = extrair_entidades(pergunta)
    num_total = len(entidades)

    mencionadas = [
        e for e in entidades if re.search(rf"\b{e}\b", resposta_norm)
    ]
    num_mencionadas = len(mencionadas)

    conjuncao_e = " e " in pergunta_norm

    quantificadores = ["todos","todas","ninguém","nenhum","todo mundo"]
    tem_quantificador = any(q in resposta_norm for q in quantificadores)

    # --- SUBINFORMATIVA ---
    if conjuncao_e and 0 < num_mencionadas < num_total:
        return "subinformativa"

    # --- SOBREINFORMATIVA ---
    if tem_quantificador:
        return "sobreinformativa"

    # --- COMPLETA explícita ---
    if conjuncao_e and num_mencionadas == num_total:
        return "completa"

    # --- COMPLETA simples (1 entidade) ---
    if num_total == 1 and num_mencionadas == 1:
        return "completa"

    return "indefinida"

dados = [
    ["O João e a Maria foram à festa?", "A Maria foi."],
    ["O João foi à festa?", "Todos foram."],
    ["O João e a Maria foram à festa?", "O João e a Maria foram."],
    ["A Maria fala japonês?", "Sim."],
    ["A Maria fala japonês?", "Sim, fala."],
    ["O João e a Maria foram à festa?", "Sim."],
    ["Os alunos e os professores participaram?", "Os professores participaram."],
]

df = pd.DataFrame(dados, columns=["pergunta","resposta"])
df["categoria"] = df.apply(
    lambda x: classificar_informatividade(x["pergunta"], x["resposta"]),
    axis=1
)

print(df)


