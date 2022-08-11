![image](img/talend-logo.png)

---

> Guia básico para utilização da ferramenta Talend.

Este guia tem como objetivo dar uma visão geral, conceitos básicos com foco em integrações de dados do tipo ETL e irá abordar o básico para que você possa desenvolver o seu primeiro Job

> Criando um projeto.

Por padrão, a ferramenta vem com a opção "Create a new project" selecionada e é possível também importar um projeto de
demonstração ou um projeto desenvolvido previamente no Talend.

![image](img/1_project.png)

> Visão Geral

Após criar o projeto, você estará frente a uma tela como essa.
![image](img/visao_geral.png)

1. Repositório
   <br>
   Local para armazenamento de Jobs, contextos, metadados e
   documentações.

2. Design Workspace
   <br>
   É onde serão “desenhados” os Jobs, dando acesso à visualização gráfica dos Processos
   de Integração em forma de fluxogramas.

3. Paleta de Componentes
   <br>
   Contém os componentes disponíveis para desenvolver os Jobs.
   Cada componente tem um propósito específico, como fazer
   uma ação no banco de dados, ler um arquivo, fazer o mapeamento de campos, mesclar colunas e etc.

4. Abas de Configuração
   <br>
   Cada aba tem uma função específica para configuração de propriedades do elemento
   que está selecionado dentro do Design Workspace.  
   Component – configuração de cada componente.  
   Context – para definição de parâmetros que variam
   de acordo com o contexto de execução.  
   Run – para execução dos Jobs e visualização passo à passo do que acontece no fluxograma desenhado.

5. Visão
   <br>
   Permite ter uma visão geral dos componentes utilizados no Job e visualizar o trecho de código fonte do componente selecionado.

> Alguns dos principais componentes do Talend Open Studio.

tFileArchive: Compacta um ou mais arquivos no formato ZIP.  
tFileUnarchive: Descompacta um ou mais arquivos no formato
_.tar.gz , _.tgz, _.tar, _.gz and \*.zip.  
tFileCompare: Componente criado para comparar dois arquivos.  
tFileCopy: Serve para copiar um ou mais arquivos entre diretórios.  
tFileDelete: Serve para deletar um ou mais arquivos entre diretórios.  
tFileExist: Verifica se um determinado arquivo existe.  
tFileRowCount: Conta a quantidade de linhas de um arquivo.  
tAggregateRow: Componente criado para agregar dados em um arquivo ou tabela do banco de dados.  
tReplace: Executa uma operação de Pesquisa e Substituição
em colunas.  
tFilterRow: Filtra registros dentro de um arquivo ou tabela.
tSplitRow: Transforma linhas em colunas.

> Lab Dataxptz: Renda de Filmes Brasileiros por Diretor.

1. Definição de Metadados

A primeira etapa consiste na definição dos metadados que serão
utilizadas na implementação do processo ETL. Neste caso de uso você irá ter duas fontes
heterogêneas: um arquivo delimitado do tipo CSV e um arquivo Excel.

![image](img/create_file_delimited.png)

Um assistente para definição dos metadados irá se abrir. Especifique o nome, propósito e
descrição do arquivo CSV utilizando como referência a imagem a seguir.

![image](img/create_file_delimited_1.png)

No segundo passo você irá configurar o caminho para leitura do arquivo. Uma pré-visualização será exibida na tela

![image](img/create_file_delimited_2.png)

No terceiro passo do assistente para definição de metadados, você irá conseguir configurar o Encoding, Habilitar o cabeçalho (Header) e poderá acompanhar as modificações clicando em "Refresh Preview".

![image](img/create_file_delimited_3.png)

O último passo consiste na definição dos metadados de cada coluna. (Integer/inteiro, String/texto, Float/decimal etc.), você pode revisar os metadados deduzidos pelo Talend e alterar o que achar
necessário.

> Configurando metadados a partir de uma planilha do excel

Para configurar os metadados do segundo arquivo utilizado neste caso de uso, vá até o Repositório, Metadata e, em seguida, clique com o botão direito em File Excel e selecione a opção Create file Excel.

![image](img/create_file_excel.png)

Um novo assistente para definição de metadados irá se iniciar.

![image](img/create_file_excel1.png)

Selecione a planilha para ser lida

![image](img/create_file_excel2.png)

Pode ser que precise instalar alguns módulos, clique em Download and install all modules available e siga normalmente.

![image](img/create_file_excel3.png)

O próximo passo permite a configuração de Encoding (UTF-8, ISO etc.), Cabeçalho etc.

![image](img/create_file_excel4.png)

No último passo você irá configurar o nome das colunas e revisar os tipos de dados. O Talend atribui automaticamente aos metadados o nome da coluna como no Excel (A, B, C...), mas para facilitar a compreensão dos dados no futuro e permitir um mapeamento mais claro em seus Jobs, você pode atribuir manualmente o nome das colunas.

![image](img/create_file_excel5.png)

> Criando job para integração de dados.

![image](img/create_job.png)

Atribua um nome, propósito e descrição.

![image](img/job_renda_filmes_por_diretor.png)

> Extração de dados.

Clique no file delimited e arraste para o Design Workspace

![image](img/arraste_file_delimited.png)

Uma janela irá surgir permitindo a seleção de qual componente você deseja utilizar

![image](img/file_input_filmes.png)

Após adicionar o tFileInputDelimited ao Job, clique com o botão direito sobre o componente e arraste o cursor para a direita. Você irá observar que o ícone de um plugue irá surgir próximo ao cursor.  
Ao soltar o botão direito, uma caixa irá surgir para que você possa pesquisar pelo componente que deseja conectar ao tFileInputDelimited. Pesquise pelo termo log e então clique duas vezes sobre a opção tLogRow.

![image](img/tLogRow1.png)

O tLogRow é um componente muito útil para analisar o que está acontecendo com os dados entre um componente e outro, permitindo identificar possíveis erros durante a execução do Job.  
Ao executar o Job clicando na aba Run. Você irá observar que o conteúdo do arquivo CSV irá aparecer na tela de log.

![image](img/tLogRow.png)

> Realizando mapeamento

Expanda a seção Processing da Paleta de Componentes e em seguida arraste o componente tMap para próximo do componente tLogRow.  
Clique com o botão direito sobre o componente tLogRow. No menu de contexto,
aponte para o submenu Row e então selecione a opção Main. Clique sobre o componente
tMap para conectá-lo ao restante do fluxo.  
Em seguida você irá adicionar ao Job a Planilha Excel de Metadados. Vá até o Repositório, expanda a seção Metadata e então Arraste a
conexão criada anteriormente até o Job, como na imagem a seguir.

![image](img/map_fluxo_excel.png)

Em seguida, conecte o componente tFileInputExcel ao tMap adicionado anteriormente.

![image](img/map1.png)

Clique duas vezes no componente tMap para abrir a janela de configuração dos mapeamentos.

![image](img/dois_clicks_map.png)

No lado esquerdo desta janela você terá as duas entradas conectadas ao componente tMap, a primeira delas irá apresentar todas as colunas do arquivo CSV com informações de filmes e a segunda apresentará as colunas do arquivo Excel.

Você irá configurar uma junção (join) entre estas duas entradas. Clique sobre o atributo Direcao e arraste-o até o atributo Nome_Diretor

![image](img/juncao_direcao_nome_diretor.png)

No lado direito do componente tMap você irá configurar a saída de dados. Clique sobre o ícone + para adicionar uma tabela de saída e então atribua o nome.  
O próximo passo consiste em arrastar as colunas desejadas para a saída. Selecione e arraste as colunas ID_Diretor e Nome_Diretor do arquivo Excel; em seguida, arraste as colunas Renda e Publico do arquivo CSV para a tabela à direita do componente tMap. O resultado será semelhante ao mapeamento na imagem abaixo:

![image](img/juncoes_saida.png)

> Agrupamentos, cálculos e ordenação.

Leve o cursor um pouco à direita do componente tMap e clique na área de desenho do Job.  
Então, na caixa de pesquisa que irá aparecer, pesquise pelo termo “aggregate”. Clique duas vezes no componente tAggregateRow para adicioná-lo.

![image](img/aggregate.png)

Agora você irá configurar as agregações de dados e os cálculos realizados.  
Na aba Component, clique em Sync columns;  
Em seguida clique duas vezes no ícone + para incluir as colunas ID_Diretor e Nome_Diretor na seção Group by;  
Depois, em Operations, clique duas vezes no ícone + para adicionar as duas colunas restantes (Renda e Publico);  
Em Function, selecione a função sum na coluna Renda para obter a renda total por diretor e avg na coluna Publico, para calcular a média de público por diretor.

![image](img/config_tAggregate.png)

Adicione um novo tLogRow após o componente tAggregateRow. Em seguida, clique na aba Component para configurar este tLogRow e selecione a opção Table como na imagem a seguir.
Isto possibilita uma visualização mais compreensível dos dados exibidos no log.

![image](img/tLogRowTabular.png)

Execute o Job pressionando F6

![image](img/tLogRowTabular_resultado.png)

Para ordenar os dados utilizaremos o componente tSortRow, volte à área de Design do Job e clique na linha entre os componentes tAggregateRow_1 e
tLogRow_2; você irá notar que alguns pontos irão aparecer demarcando a seleção da linha na qual você clicou. Em seguida, digite o termo “sort” e irá aparecer uma caixa para seleção de
componentes.

![image](img/tSortRow.png)

Agora é necessário configurar o critério de ordenação dos dados. Clique no componente tSortRow_1 e, na aba Component, clique uma vez sobre o ícone + para adicionar a coluna ID_Diretor.

Execute novamente o Job pressionando F6

![image](img/dados_ordenados.png)

> Left / inner join e tratamento de erros.

Observe que a primeira linha da tabela apresentou valores null. Isso significa que um determinado número de filmes não encontraram um diretor correspondente.  
Volte ao componente tMap e clique duas vezes sobre ele para abrir a tela de configuração de
mapeamentos. Em seguida, na opção Join Model, altere a configuração de Left Outer Join para Inner Join.

![image](img/inner_join.png)

Clique em Ok para finalizar as configurações de mapeamento e fechar a tela de configuração
do tMap. Em seguida execute novamente o Job pressionando F6.

Mensagens em vermelho continuarão a aparecer no log, como abaixo:

![image](img/log_error.png)

Estes erros são relacionados à incompatibilidade de tipos numéricos com dados não-numéricos e isto quer dizer que os metadados do arquivo informam ao Talend que ele deve
aguardar um valor numérico em uma determinada coluna, mas na verdade ele encontrou um texto.

Clique com o botão direito no componente tFileInputDelimited e então, no menu de contexto
que irá aparecer, aponte para a seção Row e clique em Reject.

![image](img/rejeitados.png)

Em seguida, clique em uma área qualquer do Job. Um menu para seleção de componentes irá
aparecer e você irá pesquisar pelo componente tLogRow. Clique duas vezes neste componente
para adicioná-lo ao Job.  
Agora você irá implementar uma segunda captura de dados rejeitados.

> Capturando dados rejeitados.

Para que você possa identificar quais filmes do arquivo CSV não possuem um diretor correspondente na planilha Excel, volte ao componente tMap e clique duas vezes sobre ele.  
Na tela de configuração de mapeamentos, no lado direito, clique no ícone + para
adicionar uma nova tabela de saída (add output table); dê a ela o nome
“filmes_rejeitados”.  
Em seguida, arraste todos os campos da tabela de filmes à esquerda para a nova
tabela criada à direita.  
Por fim, clique no primeiro ícone sobre a tabela “filmes_rejeitados” (tMap settings);  
Altere para true a configuração Catch lookup inner join reject.

![image](img/filmes_rejeitados.png)

Clique com o botão direito sobre o componente tMap e no menu de contexto, abaixo da
opção Row, irá surgir uma conexão com o mesmo nome da tabela que você criou
(“filmes_rejeitados”). Selecione esta opção e conecte-a a um novo componente tLogRow.
Execute novamente o Job e observe os resultados obtidos.  
Por fim utilize tFileOutputDelimited para escrever em um
arquivo CSV e com um tDBOutput poderá criar um banco de dados a partir dos dados gerados.

![image](img/fim.png)
