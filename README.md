Teste técnico realizado para uma empresa para o cargo de Engenheiro de Dados, o objetivo é de desenvolver uma captura de dados do site oficial do Diário da União (https://www.in.gov.br/leiturajornal) sobre os dados que a ANVISA publica regularmente sobre deferir os registros e as petições dos produtos saneantes. A captura tem que ser feita utilizando Python, e após a captura é necessário realizar o tratamento dos dados e a exportação dessas tabelas para um arquivo Excel. Após isso, é necessário desenvolver um modelo de dados para armazenar essas informações e um processo recorrente de captura e armazenamento.

O primeiro passo é estudar o comportamento do site que será minerado, após inspecionar o site, é possível verificar que todas as informações estão dentro de tags iguais (p), e que todas as colunas, tirando a resolução, também possuem a mesma classe: dou-paragraph. Ao verificar isso, o próximo passo é minerar todas as tags (p) de maneira não estruturada, e então processar essas informações separadamente e adicionar elas a uma tabela de dados em formato xlsx (Excel).

Para pegar a lista de url's que será minerada, foi feita uma pesquisa personalizada no diário da união, buscando os resultados para a pesquisa: "deferir os registros e as petições dos produtos saneantes" no período de janeiro e fevereiro de 2022, após isso foi criada a lista de urls manualmente com essas url's encontradas.

PS: A resolução de número 4866, datada no dia 30/12/2021 aparece na Edição N-1 na pesquisa personalizada entre os meses de janeiro e fevereiro porque a edição foi postada no dia 03/01/2022, mas será retirada da planilha visto que a resolução é de dezembro. Se for necessário obter os dados desse dia, é necessário recolocar essa url na variável lista_urls.

Após minerar todos os dados das páginas e verificar o tamanho de cada lista, é possível começar a entender os dados e começar a planejar o nosso banco de dados. Foi possível verificar que só possuem 6 resultados de resoluções, uma para cada resultado; A quantidade de nomes de empresas e autorizações será sempre o mesmo; Nem todos os produtos irão possuir um expediente, será quase metade deles que irão possuir um apenas; Nem todos os produtos possuem um vencimento, porém é muito raro; Não existe nenhum valor único dentro da base de dados para ser usado como Primary Key

Transformações sugeridas para os dados: 
-Padronizar a coluna Validade do Produto para o mesmo período de tempo (como o menor período é de dias, vai ser o padrão)

-Separar a coluna resolução em duas colunas: Número da resolução (int) e Data da resolução (Datetime) 

-Transformar todos os registros em letras maiúsculas  

-Transformar todos os valores desconhecidos (como o 000 nos registros, e o valor em branco em outras categorias) em valores nulos

-Transformar a coluna de vencimento para datetime

-Dividir a coluna categoria em Id e Classe da categoria 

Tecnologias utilizadas: Python, Requests, BeautifulSoup, Pandas, Numpy e SQL
