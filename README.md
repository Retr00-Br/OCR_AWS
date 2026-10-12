# OCR_AWS

Esse projeto tem como finalidade explicar as funcionalidades do OCR aplicado à AWS (Textract) para uma análise fluida dos campos de documentos, podendo ser extraídos os dados para banco de dados, planilhas ou outros sistemas para armazenamento de dados

---

## Analise do contexto - Utilização de sistemas de OCR e aumento na performance de trabalho

Percebemos tarefas repetitivas no dia à dia em nossos trabalho, podemos ficar com a ideia de "podemos automatizar isso?", para isso, sistemas inteligentes de OCR tem sua aplicabilidade. 
Sistemas OCR são leitores ópticos de imagens para textos, onde ele realiza a leitura através de comandos, lendo campos específicos de campos de um documento, podendo extrair os dados e filtrar informações importantes do documento carregado.
A AWS tem sua plataforma para solucionar esses problemas, chamada AWS Textract, cujo faz essa leitura por IA dos documentos, mesmo o documento com uma claridade alta ou até mesmo digitalizado torto, a IA é treinada para que a leitura ocorra normalmente, assim, mitigando possíveis erros e retrabalhos humanos.

---

## O que eu aprendi e apliquei nesse projeto?

1. **O que é OCR e os Diferenciais do Amazon Textract:**
   * Entendi a evolução do OCR tradicional (que apenas "enxerga" letras) para soluções de IA que estruturam e compreendem o layout de documentos complexos (como tabelas e formulários).

2. **Configuração via AWS CLI (Linux e Windows):**
   * Pratiquei a configuração de credenciais e a criação de projetos na nuvem utilizando a linha de comando (`aws configure`), garantindo agilidade no setup.

3. **Integração com Python:**
   * Uso da biblioteca padrão da AWS (`boto3`) para interagir programmaticamente com o serviço.

4. **Análise de Documentos e Objetos de Resposta:**
   * Exploração do método `Analyze Document`, entendendo o formato JSON de resposta que a API devolve (blocos, linhas, palavras, relações de chave-valor e confiança da IA).

5. **Extração e Exibição de Dados:**
   * Desenvolvimento do código em Python para varrer as respostas da IA, relacionar chaves com seus respectivos valores e exibir isso de forma limpa no console.

---

## Código realizado
import boto3

def analisar_documento(nome_arquivo):
    # Inicializa o cliente do Textract
    client = boto3.client('textract')

    # Leitura do arquivo de imagem local no Colab
    with open(nome_arquivo, 'rb') as file:
        img_bytes = file.read()

    # Chamada da API AnalyzeDocument
    response = client.analyze_document(
        Document={'Bytes': img_bytes},
        FeatureTypes=['FORMS', 'TABLES']
    )

    print(f"Documento analisado com sucesso! Total de blocos encontrados: {len(response['Blocks'])}")

    # Exemplo de extração simples dos blocos de texto encontrados
    for block in response['Blocks']:
        if block['BlockType'] == 'LINE':
            print(f"Texto encontrado: {block['Text']}")

if __name__ == '__main__':
    analisar_documento('CMS1500-sample.png')
