---
title: Suporte a agrupamentos e a Unicode | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- binary collations [SQL Server]
- expression-level collations [SQL Server]
- Windows collations [SQL Server]
- globalization [SQL Server], about globalization
- supplementary character support
- code pages [SQL Server], about code pages
- collations [SQL Server], about collations
- Unicode [SQL Server], collations
- database-level collations [SQL Server]
- reading order
- column-level collations
- locales [SQL Server], about locales
- locales [SQL Server]
- code pages [SQL Server]
- SQL Server collations
- server-level collations [SQL Server]
ms.assetid: 92d34f48-fa2b-47c5-89d3-a4c39b0f39eb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c63b7c0d1acad34bb273e4a49921d55818965e80
ms.sourcegitcommit: 82a1ad732fb31d5fa4368c6270185c3f99827c97
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/21/2019
ms.locfileid: "72688731"
---
# <a name="collation-and-unicode-support"></a>Suporte a ordenações e a Unicode
  Os agrupamentos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornecem propriedades de classificação, regras de caso e de sensibilidade a acentos para seus dados. Agrupamentos que são usados com tipos de dados de caractere como `char` e `varchar` ditam a página de código e os caracteres correspondentes que podem ser representados para esse tipo de dados. Se você estiver instalando uma nova instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], restaurando um backup de banco de dados ou conectando o servidor aos bancos de dados do cliente, é importante entender os requisitos de localidade, a ordem de classificação e a diferenciação de maiúsculas e minúsculas e a distinção de acentos que você será trabalhando com. Para listar os agrupamentos disponíveis em sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Sys. &#40;FN_HELPCOLLATIONS Transact-&#41;SQL](/sql/relational-databases/system-functions/sys-fn-helpcollations-transact-sql).  
  
 Quando você seleciona um agrupamento para seu servidor, banco de dados, coluna ou expressão, você atribui determinadas características aos dados que afetarão os resultados de muitas operações no banco de dado. Por exemplo, quando você constrói uma consulta usando ORDER BY, a ordem de classificação do seu conjunto de resultados pode depender do agrupamento que é aplicado ao banco de dados ou ditado em uma cláusula COLLATE no nível de expressão da consulta.  
  
 Para usar melhor o suporte a agrupamentos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você deve entender os termos definidos neste tópico e como eles se relacionam com as características de seus dados.  
  
  
###  <a name="Collation_Defn"></a>Agrupamento  
 Um agrupamento especifica os padrões de bits que representam cada caractere em um conjunto de dados. Os agrupamentos também determinam as regras que classificam e comparam os dados. o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte ao armazenamento de objetos que têm agrupamentos diferentes em um único banco de dados. Para colunas não-Unicode, a configuração de agrupamento especifica a página de código para os dados e quais caracteres podem ser representados. Os dados movidos entre colunas não-Unicode devem ser convertidos da página de código-fonte para a página de código de destino.  
  
 os resultados da instrução de [!INCLUDE[tsql](../../includes/tsql-md.md)] podem variar quando a instrução é executada no contexto de bancos de dados diferentes que têm configurações de agrupamento diferentes. Se possível, use um agrupamento padronizado para sua organização. Dessa forma, você não precisa especificar explicitamente o agrupamento em cada caractere ou expressão Unicode. Se você precisar trabalhar com objetos que têm diferentes configurações de agrupamento e página de código, codifique suas consultas para considerar as regras de precedência de agrupamento. Para obter mais informações, consulte [precedência de agrupamento (Transact-SQL)](/sql/t-sql/statements/collation-precedence-transact-sql).  
  
 As opções associadas a um agrupamento diferenciam maiúsculas de minúsculas, diferencia acentos, diferencia caracteres kana, sensibilidade de largura. Estas opções são especificadas através de sua anexação ao nome de ordenação. Por exemplo, esse agrupamento `Japanese_Bushu_Kakusu_100_CS_AS_KS_WS` diferencia maiúsculas de minúsculas, diferencia acentos, diferencia caracteres kana e diferencia largura. A tabela a seguir descreve o comportamento associado a essas opções.  
  
|Option|Description|  
|------------|-----------------|  
|Diferenciar maiúsculas de minúsculas (_CS)|Distingue entre letras maiúsculas e minúsculas. Se selecionado, as letras minúsculas são classificadas à frente de suas versões em maiúsculas. Se essa opção não for selecionada, o agrupamento não diferenciará maiúsculas de minúsculas. Ou seja, SQL Server considera que as versões maiúsculas e minúsculas de letras são idênticas para fins de classificação. Você pode selecionar explicitamente a não diferenciação de maiúsculas e minúsculas especificando _CI.|  
|Diferenciar acentos (_AS)|Faz distinção entre caracteres acentuados e não acentuados. Por exemplo, ' a ' não é igual a '&#x1EA5;'. Se essa opção não estiver selecionada, o agrupamento não fará diferenciação de acentos. Ou seja, o SQL Server considera as versões com e sem acentos como idênticas para fins de classificação. Você pode selecionar explicitamente a não diferenciação de acento especificando _AI.|  
|Diferenciar Kana (_KS)|Distingue entre os dois tipos de caracteres kana japoneses: hiragana e Katakana. Se essa opção não estiver selecionada, o agrupamento não diferenciará kana. Ou seja, o SQL Server considera que caracteres hiragana e katakana são iguais para fins de classificação. Omitir essa opção é o único método de especificar a não diferenciação de kana.|  
|Diferenciar largura (diante)|Distingue entre caracteres de largura inteira e de meia largura. Se essa opção não estiver selecionada, SQL Server considerará que a representação de largura inteira e de meia largura do mesmo caractere é idêntica para fins de classificação. Omitir essa opção é o único método de especificar a não diferenciação de largura.|  
  
 o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte aos seguintes conjuntos de agrupamento:  
  
 Agrupamentos do Windows  
 Os agrupamentos do Windows definem regras para armazenar dados de caractere que se baseiam em uma localidade de sistema do Windows associada. Para um agrupamento do Windows, a comparação de dados não-Unicode é implementada usando o mesmo algoritmo que os dados Unicode. As regras básicas de agrupamento do Windows especificam qual alfabeto ou idioma é usado quando a classificação de dicionário é aplicada e a página de código usada para armazenar dados de caracteres não Unicode. A classificação Unicode e não-Unicode é compatível com comparações de cadeia de caracteres em uma versão específica do Windows. Isso proporciona consistência entre os tipos de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e também permite que os desenvolvedores classifiquem as cadeias de caracteres nos aplicativos usando as mesmas regras utilizadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [nome &#40;de agrupamento do Windows&#41;Transact-SQL](/sql/t-sql/statements/windows-collation-name-transact-sql).  
  
 Agrupamentos binários  
 Os agrupamentos binários classificam dados com base na sequência de valores codificados que são definidos pela localidade e pelo tipo de dados. Eles fazem diferenciação de maiúsculas e minúsculas. Um agrupamento binário no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] define a localidade e a página de código ANSI que será usada. Isso impõe uma ordem de classificação binária. Como são relativamente simples, os agrupamentos binários ajudam a melhorar o desempenho do aplicativo. Para tipos de dados não-Unicode, as comparações de dados são baseadas nos pontos de código definidos na página de código ANSI. Para tipos de dados Unicode, as comparações de dados são baseadas nos pontos de código Unicode. Para ordenações primárias em tipos de dados Unicode, a localidade não é considerada em classificações de dados. Por exemplo, Latin_1_General_BIN e Japanese_BIN produzem resultados de classificação idênticos quando são usados em dados Unicode.  
  
 Há dois tipos de agrupamentos binários no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; os agrupamentos de `BIN` mais antigos e os agrupamentos de `BIN2` mais recentes. Em um agrupamento de `BIN2`, todos os caracteres são classificados de acordo com seus pontos de código. Em um `BIN` agrupamento somente o primeiro caractere é classificado de acordo com o ponto de código, e os caracteres restantes são classificados de acordo com seus valores de byte. (Como a plataforma Intel é uma arquitetura de little endian, os caracteres de código Unicode sempre são armazenados em troca de bytes.)  
  
 Agrupamentos de SQL Server  
 agrupamentos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQL_ *) fornecem compatibilidade de ordem de classificação com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. As regras de classificação de dicionário para dados não-Unicode são incompatíveis com qualquer rotina de classificação fornecida pelos sistemas operacionais Windows. No entanto, a classificação de dados Unicode é compatível com uma versão específica das regras de classificação do Windows. Como os agrupamentos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usam regras de comparação diferentes para dados não Unicode e Unicode, você verá resultados diferentes para comparações dos mesmos dados, dependendo do tipo de dados subjacente. Para obter mais informações, consulte [SQL Server nome &#40;do agrupamento Transact&#41;-SQL](/sql/t-sql/statements/sql-server-collation-name-transact-sql).  
  
> [!NOTE]
>  Quando você atualiza uma instância em inglês do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agrupamentos (SQL_ *) podem ser especificados para compatibilidade com as instâncias existentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Como a ordenação padrão de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é definida durante a instalação, é importante especificar as configurações de ordenação com cuidado quando as seguintes afirmações forem verdadeiras:  
> 
>  -   O código do aplicativo depende do comportamento dos agrupamentos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores.  
> -   Você deve armazenar dados de caractere que refletem vários idiomas.  
  
 Há suporte para a configuração de agrupamentos nos seguintes níveis de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
 Agrupamentos no nível do servidor  
 O agrupamento padrão do servidor é definido durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e também se torna o agrupamento padrão dos bancos de dados do sistema e de todos os bancos de dados de usuário. Observe que os agrupamentos somente Unicode não podem ser selecionados durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] porque não têm suporte como agrupamentos de nível de servidor.  
  
 Depois que um agrupamento tiver sido atribuído ao servidor, você não poderá alterar o agrupamento, exceto pela exportação de todos os objetos e dados do banco de dados, recriando o banco de dado `master` e importando todos os objetos e dados do banco de dados. Em vez de alterar o agrupamento padrão de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode especificar o agrupamento desejado no momento em que cria um novo banco de dados ou coluna de banco de dados.  
  
 Agrupamentos no nível do banco de dados  
 Quando um banco de dados é criado ou modificado, você pode usar a cláusula COLLATE da instrução CREATE DATABASE ou ALTER DATABASE para especificar o agrupamento de banco de dados padrão. Se nenhum agrupamento for especificado, o banco de dados será atribuído ao agrupamento do servidor.  
  
 Você não pode alterar o agrupamento de bancos de dados do sistema, exceto alterando o agrupamento para o servidor.  
  
 O agrupamento de banco de dados é usado para todos os metadados no banco de dados, e é o padrão para todas as colunas de cadeia de caracteres, objetos temporários, nomes de variáveis e outras cadeias usadas no banco de dados. Quando você altera o agrupamento de um banco de dados de usuário, pode haver conflitos de agrupamento quando as consultas no banco de dados acessam tabelas temporárias. As tabelas temporárias são sempre armazenadas no banco de dados do sistema `tempdb`, que usará o agrupamento para a instância. As consultas que comparam dados de caractere entre o banco de dado do usuário e `tempdb` poderão falhar se os agrupamentos causarem um conflito na avaliação dos dados de caractere. Você pode resolver isso especificando a cláusula COLLATE na consulta. Para obter mais informações, consulte [COLLATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/collations).  
  
 Agrupamentos em nível de coluna  
 Ao criar ou alterar uma tabela, você pode especificar agrupamentos para cada coluna de cadeia de caracteres de caractere usando a cláusula COLLATE. Se nenhuma ordenação for especificada, a ordenação padrão do banco de dados será atribuída à coluna.  
  
 Agrupamentos em nível de expressão  
 Os agrupamentos em nível de expressão são definidos quando uma instrução é executada e afetam a maneira como um conjunto de resultados é retornado. Isso permite que os resultados da classificação ORDER BY sejam específicos da localidade. Use uma cláusula COLLATE como a seguinte para implementar agrupamentos em nível de expressão:  
  
```  
SELECT name FROM customer ORDER BY name COLLATE Latin1_General_CS_AI;  
```  
  
  
###  <a name="Locale_Defn"></a>Localidade  
 Uma localidade é um conjunto de informações associadas a um local ou a uma cultura. Isso pode incluir o nome e o identificador do idioma falado, o script usado para escrever o idioma e as convenções culturais. Os agrupamentos podem ser associados a uma ou mais localidades. Para obter mais informações, consulte [IDs de localidade atribuídas pela Microsoft](https://msdn.microsoft.com/goglobal/bb964664.aspx).  
  
  
###  <a name="Code_Page_Defn"></a>Página de código  
 Uma página de código é um conjunto ordenado de caracteres de um determinado script no qual um índice numérico, ou valor de ponto de código, está associado a cada caractere. Uma página de código do Windows é normalmente conhecida como um *conjunto de caracteres* ou *charset*. As páginas de código são usadas para fornecer suporte para os conjuntos de caracteres e layouts de teclado usados por diferentes localidades do sistema Windows.  
  
  
###  <a name="Sort_Order_Defn"></a>Ordem de classificação  
 Ordem de classificação especifica como os valores de dados são classificados. Isso afeta os resultados da comparação de dados. Os dados são classificados usando agrupamentos e podem ser otimizados usando índices.  
  
  
##  <a name="Unicode_Defn"></a>Suporte a Unicode  
 O Unicode é um padrão para mapear pontos de código para caracteres. Como ele foi projetado para abranger todos os caracteres de todos os idiomas do mundo, não há necessidade de páginas de código diferentes para lidar com conjuntos de caracteres diferentes. Se você armazenar dados de caractere que refletem vários idiomas, sempre use os tipos de dados Unicode (`nchar`, `nvarchar` e `ntext`) em vez dos tipos de dados não-Unicode (`char`, `varchar` e `text`).  
  
 Limitações significativas são associadas a tipos de dados não-Unicode. Isso ocorre porque um computador não-Unicode será limitado ao uso de uma única página de código. Você pode experimentar o desempenho usando Unicode porque são necessárias menos conversões de página de código. As ordenações Unicode devem ser selecionadas individualmente no nível de banco de dados, coluna ou expressão porque não têm suporte no nível de servidor.  
  
 As páginas de código que um cliente usa são determinadas pelas configurações do sistema operacional. Para definir as páginas de código do cliente no sistema operacional Windows, use **Configurações regionais** no painel de controle.  
  
 Quando você move dados de um servidor para um cliente, a ordenação do servidor pode não ser reconhecida por drivers de cliente mais antigos. Isso pode ocorrer quando você move dados de um servidor Unicode para um cliente não Unicode. A melhor opção pode ser atualizar o sistema operacional do cliente para que os agrupamentos subjacentes do sistema sejam atualizados. Se o cliente tiver o software cliente do banco de dados instalado, você poderá considerar a aplicação de uma atualização de serviço ao software cliente do banco de dados.  
  
 Você também pode tentar usar um agrupamento diferente para os dados no servidor. Escolha uma ordenação que será mapeada para uma página de código no cliente.  
  
 Para usar os agrupamentos UTF-16 disponíveis no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], você pode selecionar um dos caracteres suplementares `_SC` agrupamentos (somente agrupamentos do Windows) para melhorar a pesquisa e a classificação de alguns caracteres Unicode.  
  
 Para avaliar os problemas relacionados ao uso de tipos de dados Unicode ou não-Unicode, teste seu cenário para medir as diferenças de desempenho em seu ambiente. É uma prática recomendada padronizar o agrupamento que é usado em sistemas em toda a sua organização e implantar servidores e clientes Unicode sempre que possível.  
  
 Em muitas situações, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] irá interagir com outros servidores ou clientes, e sua organização poderá usar vários padrões de acesso a dados entre aplicativos e instâncias de servidor. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] clientes são um dos dois tipos principais:  
  
-   **Clientes Unicode** que usam OLE DB e ODBC (conectividade aberta de banco de dados) versão 3,7 ou uma versão posterior.  
  
-   **Clientes não Unicode** que usam o DB-Library e a versão 3,6 do ODBC ou uma versão anterior.  
  
 A tabela a seguir fornece informações sobre como usar dados multilíngues com várias combinações de servidores Unicode e não Unicode.  
  
|Server|Cliente|Benefícios ou limitações|  
|------------|------------|-----------------------------|  
|Unicode|Unicode|Como os dados Unicode serão usados em todo o sistema, este cenário fornece o melhor desempenho e proteção contra danos de dados recuperados. Essa é a situação com ActiveX Data Objects (ADO), OLE DB e ODBC versão 3,7 ou uma versão posterior.|  
|Unicode|Não Unicode|Neste cenário, principalmente em conexões entre um servidor que executa um sistema operacional mais recente e um cliente com uma versão mais antiga do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ou em um sistema operacional mais antigo, pode haver limitações ou erros quando você move os dados para um computador cliente. Os dados Unicode no servidor tentarão mapear para uma página de código correspondente no cliente não Unicode para converter os dados.|  
|Não Unicode|Unicode|Esta não é uma configuração ideal para usar dados multilíngues. Não é possível gravar dados Unicode no servidor não-Unicode. É provável que ocorram problemas quando os dados forem enviados para servidores que estejam fora da página de código do servidor.|  
|Não Unicode|Não Unicode|Este é um cenário muito limitado para dados multilíngues. Você pode usar apenas uma única página de código.|  
  
  
##  <a name="Supplementary_Characters"></a>Caracteres suplementares  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece tipos de dados como `nchar` e `nvarchar` para armazenar dados Unicode. Esses tipos de dados codificam o texto em um formato chamado *UTF-16*. O consórcio Unicode aloca cada caractere um ponto exclusivo, que é um valor no intervalo 0x0000 a 0x10FFFF. Os caracteres usados com mais frequência têm valores ponto que se ajustarão a uma palavra de 16 bits na memória e no disco, mas os caracteres com valores de ponto maiores que 0xFFFF exigem duas palavras consecutivas de 16 bits. Esses caracteres são chamados de *caracteres suplementares*, e as duas palavras consecutivas de 16 bits são chamadas de *pares substitutos*.  
  
 Se você usar caracteres suplementares:  
  
-   Caracteres suplementares podem ser usados apenas em operações de comparação e ordenação em versões de ordenação 90 ou superior.  
  
-   Todos os agrupamentos de nível de _100 dão suporte à classificação linguística com caracteres suplementares.  
  
-   Os caracteres suplementares não têm suporte para uso em metadados, como em nomes de objetos de banco de dados.  
  
-   Introduzidas no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], uma nova família de agrupamentos de SC (caracteres suplementares) pode ser usada com os tipos de dados `nchar`, `nvarchar` e `sql_variant`. Por exemplo: `Latin1_General_100_CI_AS_SC`, ou se estiver usando um agrupamento em Japonês, `Japanese_Bushu_Kakusu_100_CI_AS_SC`.  
  
     O sinalizador SC pode ser aplicado a:  
  
    -   Agrupamentos da versão 90 do Windows  
  
    -   Agrupamentos da versão 100 do Windows  
  
     O sinalizador de SC não pode ser aplicado a:  
  
    -   A versão 80 agrupamentos sem controle de versão do Windows  
  
    -   Os agrupamentos binários BIN ou BIN2  
  
    -   Os agrupamentos do SQL *  
  
 A tabela a seguir compara o comportamento de alguns operadores e funções de cadeia de caracteres quando eles usam caracteres suplementares com e sem uma ordenação de SC.  
  
|Operador ou função de cadeia de caracteres|Com um agrupamento SC|Sem um agrupamento SC|  
|---------------------------------|--------------------------|-----------------------------|  
|[CHARINDEX](/sql/t-sql/functions/charindex-transact-sql)<br /><br /> [LEN](/sql/t-sql/functions/len-transact-sql)<br /><br /> [PATINDEX](/sql/t-sql/functions/patindex-transact-sql)|O par substituto de UTF-16 é contado como um único ponto.|O par substituto de UTF-16 é contado como dois íntegra.|  
|[MANTIDA](/sql/t-sql/functions/left-transact-sql)<br /><br /> [Substitua](/sql/t-sql/functions/replace-transact-sql)<br /><br /> [ORDEM](/sql/t-sql/functions/reverse-transact-sql)<br /><br /> [Certo](/sql/t-sql/functions/right-transact-sql)<br /><br /> [SUBCADEIA](/sql/t-sql/functions/substring-transact-sql)<br /><br /> [COISAS](/sql/t-sql/functions/stuff-transact-sql)|Essas funções tratam cada par substituto como um único ponto e funcionam conforme o esperado.|Essas funções podem dividir quaisquer pares substitutos e levar a resultados inesperados.|  
|[NCHAR](/sql/t-sql/functions/nchar-transact-sql)|Retorna o caractere correspondente ao valor de ponto Unicode especificado no intervalo de 0 a 0x10FFFF. Se o valor especificado estiver no intervalo de 0 a 0xFFFF, um caractere será retornado. Para valores mais altos, o substituto correspondente é retornado.|Um valor maior que 0xFFFF retorna NULL em vez do substituto correspondente.|  
|[UNICODE](/sql/t-sql/functions/unicode-transact-sql)|Retorna um ponto UTF-16 no intervalo de 0 a 0x10FFFF.|Retorna um ponto UCS-2 no intervalo de 0 a 0xFFFF.|  
|[Corresponder um caractere curinga](/sql/t-sql/language-elements/wildcard-match-one-character-transact-sql)<br /><br /> [Curinga – caracteres para os quais não corresponder](/sql/t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql)|Há suporte para caracteres suplementares para todas as operações de curingas.|Não há suporte para caracteres suplementares para essas operações curinga. Há suporte para outros operadores curinga.|  
  
  
##  <a name="GB18030"></a>Suporte a GB18030  
 O GB18030 é um padrão separado usado na República da China das pessoas para codificar caracteres chineses. No GB18030, os caracteres podem ter 1, 2 ou 4 bytes de comprimento. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece suporte para caracteres codificados em GB18030 reconhecendo-os quando eles inserem o servidor de um aplicativo do lado do cliente, convertendo-os e armazenando-os nativamente como caracteres Unicode. Depois de serem armazenados no servidor, eles são tratados como caracteres Unicode em qualquer operação subsequente. Você pode usar qualquer agrupamento do chinês, preferivelmente a versão mais recente 100. Todos os agrupamentos de nível de _100 dão suporte à classificação linguística com caracteres GB18030. Se os dados incluírem caracteres suplementares (pares substitutos), você poderá usar os agrupamentos SC disponíveis no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] para melhorar a pesquisa e a classificação.  
  
  
##  <a name="Complex_script"></a>Suporte a scripts complexos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode dar suporte à inserção, armazenamento, alteração e exibição de scripts complexos. Scripts complexos incluem o seguinte:  
  
-   Os scripts que incluem a combinação de texto da direita para a esquerda e da esquerda para a direita, como uma combinação de texto em árabe e inglês.  
  
-   Os scripts cujos caracteres mudam de forma dependendo da sua posição, ou quando combinados com outros caracteres, como caracteres árabes, índicos e tailandeses.  
  
-   Idiomas como o tailandês que exigem dicionários internos para reconhecer palavras porque não há quebras entre eles.  
  
 Os aplicativos de banco de dados que interagem com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devem usar controles que dão suporte a scripts complexos. Os controles de formulário padrão do Windows criados no código gerenciado são habilitados para script complexo.  
  
  
##  <a name="Related_Tasks"></a>Tarefas relacionadas  
  
|Agenda|Tópico|  
|----------|-----------|  
|Descreve como definir ou alterar o agrupamento da instância do SQL Server.|[Definir ou alterar o agrupamento do servidor](set-or-change-the-server-collation.md)|  
|Descreve como definir ou alterar o agrupamento de um banco de dados de usuário.|[Definir ou alterar o agrupamento de banco de dados](set-or-change-the-database-collation.md)|  
|Descreve como definir ou alterar o agrupamento de uma coluna no banco de dados.|[Definir ou alterar o agrupamento de colunas](set-or-change-the-column-collation.md)|  
|Descreve como retornar informações de ordenação ao servidor, banco de dados ou nível de coluna.|[Exibir informações de agrupamento](view-collation-information.md)|  
|Descreve como escrever instruções Transact-SQL que as tornarão mais portáteis de um idioma para outro ou que dão suporte a vários idiomas com mais facilidade.|[Escrever instruções Transact-SQL internacionais](write-international-transact-sql-statements.md)|  
|Descreve como alterar o idioma de mensagens de erro e preferências de como data, hora e dados de moeda são usados e exibidos.|[Definir um idioma de sessão](set-a-session-language.md)|  
  
  
##  <a name="Related_Content"></a>Conteúdo relacionado  
 [SQL Server a alteração de agrupamento de práticas recomendadas](https://go.microsoft.com/fwlink/?LinkId=113891)  
  
 ["SQL Server a migração de práticas recomendadas para o Unicode"](https://go.microsoft.com/fwlink/?LinkId=113890)  
  
 [Site da Web do consórcio Unicode](https://go.microsoft.com/fwlink/?LinkId=48619)  
  
## <a name="see-also"></a>Consulte também  
 [Agrupamentos de banco de dados independentes](../databases/contained-database-collations.md)    
 [Escolha um idioma ao criar um índice de texto completo](../search/choose-a-language-when-creating-a-full-text-index.md)    
 [sys. fn_helpcollations (Transact-SQL)](https://msdn.microsoft.com/library/ms187963(SQL.130).aspx)  
  
  
