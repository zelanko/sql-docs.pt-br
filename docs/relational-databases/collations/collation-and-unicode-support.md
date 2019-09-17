---
title: Suporte a ordenações e a Unicode | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
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
- UTF-8
- UTF-16
- UTF8
- UTF16
- UCS2
- server-level collations [SQL Server]
ms.assetid: 92d34f48-fa2b-47c5-89d3-a4c39b0f39eb
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1bda35d5c393eaa1e4503cb487ed19b281686364
ms.sourcegitcommit: 75fe364317a518fcf31381ce6b7bb72ff6b2b93f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/11/2019
ms.locfileid: "70908411"
---
# <a name="collation-and-unicode-support"></a>Suporte a ordenações e a Unicode
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
As ordenações em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornecem propriedades de regras de classificação, de diferenciação de maiúsculas e minúsculas e de diferenciação de acentos para seus dados. As ordenações utilizadas com tipos de dados de caractere, como **char** e **varchar**, determinam a página de código e os caracteres correspondentes que podem ser representados para o tipo de dados em questão. Independentemente de você estar instalando uma nova instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], restaurando um backup de banco de dados ou conectando o servidor a bancos de dados cliente, é importante estar ciente dos requisitos de localidade, ordem de classificação e distinção de maiúsculas e minúsculas e de acentos dos dados com os quais está trabalhando. Para listar as ordenações disponíveis na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md).    
    
Ao selecionar uma ordenação para o servidor, banco de dados, coluna ou expressão, você atribui determinadas características a seus dados que afetam os resultados de muitas operações no banco de dados. Por exemplo, ao construir uma consulta usando `ORDER BY`, a ordem de classificação de seu conjunto de resultados pode depender da ordenação aplicada ao banco de dados ou ditada em uma cláusula `COLLATE` no nível de expressão da consulta.    
    
Para usar o suporte a ordenações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da melhor maneira possível, você deve estar ciente dos termos definidos neste tópico e de como eles estão relacionados às características de seus dados.    
    
##  <a name="Terms"></a> Condições da ordenação    
    
-   [Ordenação](#Collation_Defn)    
    
-   [Localidade](#Locale_Defn)    
    
-   [Página de código](#Code_Page_Defn)    
    
-   [Ordem de classificação](#Sort_Order_Defn)    
    
###  <a name="Collation_Defn"></a> Ordenação    
Uma ordenação especifica os padrões de bit que representam cada caractere em um conjunto de dados. As ordenações também determinam as regras que classificam e comparam dados. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte ao armazenamento de objetos com ordenações diferentes em um banco de dados individual. Para colunas não Unicode, a configuração de ordenação especifica a página de códigos dos dados e quais caracteres podem ser representados. Os dados movidos entre colunas não Unicode devem ser convertidos da página de código de origem para a página de código de destino.    
    
Os resultados da instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] podem variar quando a instrução for executada no contexto de diferentes bancos de dados que tenham configurações de ordenação diferentes. Se possível, use uma ordenação padronizada para sua organização. Deste modo, não será preciso especificar a ordenação explicitamente em todo caractere ou expressão Unicode. Se você deve trabalhar com objetos que tenham configurações de ordenação e página de códigos diferentes, codifique suas consultas para considerar as regras da precedência de ordenação. Para obter mais informações, consulte [Precedência de ordenação (Transact-SQL)](../../t-sql/statements/collation-precedence-transact-sql.md).    
    
As opções associadas a uma ordenação fazem distinção de maiúsculas e minúsculas, de acentos, de caracteres Kana, de largura e de seletor de variação. O [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] introduz uma opção adicional para codificação [UTF-8](https://www.wikipedia.org/wiki/UTF-8). Estas opções são especificadas através de sua anexação ao nome de ordenação. Por exemplo, esta ordenação `Japanese_Bushu_Kakusu_100_CS_AS_KS_WS_UTF8` tem diferenciação de maiúsculas e minúsculas, de acentos, de caracteres Kana e de largura e é codificado em UTF-8. Como outro exemplo, essa ordenação `Japanese_Bushu_Kakusu_140_CI_AI_KS_WS_VSS` não diferencia maiúsculas de minúsculas, não diferencia acentos, mas faz distinção de caracteres Kana, de largura e de seletor de variação e usa codificação não Unicode. A tabela a seguir descreve o comportamento associado com estas diversas opções.    
    
|Opção|Descrição|    
|------------|-----------------|    
|Diferenciar maiúsculas de minúsculas (\_CS)|Faz distinção entre letras maiúscula e minúsculas. Se selecionada, as letras minúsculas são ordenadas à frente das versões em letras maiúsculas. Se esta opção não for selecionada, a ordenação não fará diferenciação de maiúsculas e minúsculas. Ou seja, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considera as versões de letras maiúsculas e minúsculas como idênticas para fins de classificação. Você pode selecionar explicitamente a não diferenciação de maiúsculas e minúsculas, especificando \_CI.|    
|Diferenciar acentos (\_AS)|Faz distinção entre caracteres acentuados e não acentuados. Por exemplo, 'a' não é igual a 'ã'. Se esta opção não for selecionada, a ordenação não fará diferenciação de acentos. Ou seja, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considera as versões com e sem acentos como idênticas para fins de classificação. Você pode selecionar explicitamente a não diferenciação de acentos, especificando \_AI.|    
|Diferenciar caracteres Kana (\_KS)|Distingue entre os dois tipos de caracteres kana japoneses: hiragana e katakana. Se esta opção não for selecionada, a ordenação não fará diferenciação de Kana. Ou seja, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considera que caracteres hiragana e katakana são iguais para fins de classificação. A omissão desta opção é o único método de especificar a não diferenciação de Kana.|    
|Diferenciar largura (\_WS)|Faz distinção entre caracteres de largura inteira e de meia largura. Se esta opção não for selecionada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considerará as representações de largura inteira e de meia largura do mesmo caractere como iguais para fins de classificação. A omissão desta opção é o único método de especificar a não diferenciação de largura.|    
|Distinção de seletor de variação (\_VSS) | Distingue entre vários seletores de variação ideográficos em ordenações em japonês Japanese_Bushu_Kakusu_140 e Japanese_XJIS_140 introduzido primeiro em [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]. Uma sequência de variação consiste em um caractere base e um seletor de variação adicional. Se essa opção \_VSS não for selecionada, a ordenação não fará distinção de seletor de variação e o seletor de variação não será considerado na comparação. Ou seja, o SQL Server considera caracteres criados sobre o mesmo caractere base com diferenciação de seletores de variação para serem idênticos com a finalidade de classificação. Consulte também  [Unicode Ideographic Variation Database](https://www.unicode.org/reports/tr37/)(Banco de dados de variação ideográfica Unicode). <br/><br/> Não há suporte para ordenações de Diferenciação do seletor de variação (\_VSS) em índices de pesquisa de Texto Completo. Índices de pesquisa de texto completo dão suporte apenas às opções Diferenciação de Acentos (\_AS), Diferenciação de caracteres Kana (\_KS) e Diferenciação de largura (\_WS). Os mecanismos de XML e CLR do SQL Server não dão suporte a Seletores de variação (\_VSS).
|UTF-8 (\_UTF8)|Permite que dados codificados em UTF-8 sejam armazenados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se essa opção não for selecionada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usará o formato de codificação não Unicode padrão para os tipos de dados aplicáveis.| 
    
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte aos seguintes conjuntos de ordenação:    
    
#### <a name="windows-collations"></a>ordenações do Windows    
As ordenações do Windows definem regras para o armazenamento de dados de caractere baseadas em uma localidade de sistema do Windows associada. No caso de uma ordenação do Windows, a comparação de dados não Unicode é implementada usando o mesmo algoritmo que os dados Unicode. As regras de base de ordenações do Windows especificam qual alfabeto ou idioma será usado quando a classificação de dicionário for aplicada, bem como a página de código usada para armazenar dados de caracteres não Unicode. As classificações Unicode e não Unicode são compatíveis com comparações de cadeias de caracteres em uma versão específica do Windows. Isso proporciona consistência entre os tipos de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e também permite que os desenvolvedores classifiquem as cadeias de caracteres nos aplicativos usando as mesmas regras utilizadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, veja [Nome de ordenação do Windows &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md).    
    
#### <a name="binary-collations"></a>Ordenações primárias    
Os dados classificados de ordenações primárias na sequência de valores codificados definidos pelo tipo de localidade e dados. Eles fazem diferenciação de maiúsculas e minúsculas. Uma ordenação primária no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] define a localidade e a página de código ANSI que são usadas. Isso impõe uma ordem de classificação binária. Como são relativamente simples, as ordenações primárias ajudam melhorar o desempenho de aplicativo. Para tipos de dados não Unicode, as comparações de dados têm como base os pontos de código definidos na página de código ANSI. Para tipos de dados Unicode, as comparações de dados têm como base os pontos de código Unicode. Para ordenações primárias em tipos de dados Unicode, a localidade não é considerada em classificações de dados. Por exemplo, Latin_1_General_BIN e Japanese_BIN geram resultados de classificação idênticos quando usados em dados Unicode.    
    
Existem dois tipos de ordenações primárias no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: as ordenações **BIN** mais antigas e as ordenações **BIN2** mais novas. Em uma ordenação **BIN2**, todos os caracteres são classificados de acordo com seus pontos de código. Em uma ordenação **BIN**, apenas o primeiro caractere é classificado de acordo com o ponto de código e os caracteres restantes são classificados de acordo com seus valores de byte. (Como a plataforma Intel é um arquitetura little endian, os caracteres de código Unicode são sempre trocados por bytes armazenados.)    
    
#### <a name="sql-server-collations"></a>ordenações do SQL Server    
As ordenações (SQL_\*) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferecem compatibilidade de ordem de classificação com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. As regras de classificação de dicionário para dados não Unicode são incompatíveis com rotinas de classificação fornecidas pelos sistemas operacionais Windows. No entanto, a classificação de dados Unicode é compatível com uma versão específica das regras de classificação do Windows. Como as ordenações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usam regras de comparação diferentes para dados não Unicode e Unicode, você vê resultados diferentes para comparações dos mesmos dados, dependendo do tipo de dados subjacente. Para obter mais informações, veja [Nome de ordenação do SQL Server &#40;Transact-SQL&#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md).    
    
> [!NOTE]    
> Quando você atualiza uma instância em português do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], as ordenações (SQL_\*) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem ser especificadas para compatibilidade com instâncias existentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Como a ordenação padrão de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é definida durante a instalação, é importante especificar as configurações de ordenação com cuidado quando as seguintes afirmações forem verdadeiras:    
>     
> -   Seu código de aplicativo depende do comportamento de ordenações anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].    
> -   Você deve armazenar dados de caractere que refletem vários idiomas.    
    
 Há suporte para configurar ordenações nos seguintes níveis de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:    
    
#### <a name="server-level-collations"></a>Ordenações no nível do servidor   
A ordenação do servidor padrão é definida durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e também se torna a ordenação padrão dos bancos de dados do sistema e de todos os bancos de dados de usuário. Observe que as ordenações somente Unicode não podem ser selecionadas durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], pois elas não são suportadas como ordenações no nível de servidor.    
    
Depois que uma ordenação for atribuída ao servidor, você não poderá alterar a ordenação, exceto exportando todos os objetos de banco de dados e dados, recriando o banco de dados **master** e importando todos os objetos de banco de dados e dados. Em vez de alterar a ordenação padrão de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode especificar a ordenação desejada no momento da criação de um novo banco de dados ou coluna de banco de dados.    
    
#### <a name="database-level-collations"></a>Ordenações do nível do banco de dados    
Quando um banco de dados é criado ou modificado, você pode usar a cláusula COLLATE da instrução CREATE DATABASE ou ALTER DATABASE para especificar a ordenação de banco de dados padrão. Se nenhuma ordenação for especificada, o banco de dados receberá a ordenação do servidor.    
    
Você não pode alterar a ordenação de bancos de dados do sistema, exceto alterando a ordenação para o servidor.    
    
A ordenação de banco de dados é usada para todos os metadados no banco de dados e é a padrão para todas as colunas de cadeia de caracteres, objetos temporários, nomes de variável e quaisquer outras cadeias de caracteres usadas no banco de dados. Quando você altera a ordenação de um banco de dados de usuário, pode haver conflitos de ordenação quando consultas no banco de dados acessam tabelas temporárias. Sempre são armazenadas tabelas temporárias no banco de dados do sistema **tempdb** que usa a ordenação para a instância. Consultas que comparam dados de caractere entre o banco de dados de usuário e **tempdb** poderão falhar se as ordenações causarem um conflito ao avaliar os dados de caractere. Você pode resolver isso especificando a cláusula COLLATE na consulta. Para obter mais informações, veja [COLLATE &#40;Transact-SQL&#41;](~/t-sql/statements/collations.md).    

> [!NOTE]
> A ordenação não poderá ser alterada depois que o banco de dados tiver sido criado em [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].


#### <a name="column-level-collations"></a>Ordenações em nível de coluna    
Quando você cria ou altera uma tabela, pode especificar ordenações para cada coluna de cadeia de caracteres usando a cláusula COLLATE. Se nenhuma ordenação for especificada, a ordenação padrão do banco de dados será atribuída à coluna.    
    
#### <a name="expression-level-collations"></a>Ordenações no nível da expressão    
As ordenações no nível de expressão são definidas quando uma instrução é executada e afetam o modo como um conjunto de resultados é retornado. Isso permite que os resultados da classificação ORDER BY sejam específicos de localidade. Use uma cláusula COLLATE como a seguinte para implementar ordenações no nível da expressão:    
    
```sql    
SELECT name FROM customer ORDER BY name COLLATE Latin1_General_CS_AI;    
```    
    
###  <a name="Locale_Defn"></a> Localidade    
Uma localidade é um conjunto de informações associadas a um local ou a uma cultura. Essas informações podem incluir o nome e o identificador do idioma falado, o script usado para escrever o idioma e as convenções culturais. As ordenações podem ser associadas a uma ou mais localidades. Para obter mais informações, consulte o artigo sobre [IDs de localidade atribuídas pela Microsoft](https://msdn.microsoft.com/goglobal/bb964664.aspx).    
    
###  <a name="Code_Page_Defn"></a> Code Page    
 Uma página de código é um conjunto de caracteres ordenado de um determinado script no qual um índice numérico ou valor de ponto de código é associado a cada caractere. Uma página de códigos do Windows geralmente é referenciada como um *conjunto de caracteres* ou um *charset*. As páginas de código são usadas para oferecer suporte aos conjuntos de caracteres e layouts de teclado usados por diferentes localidades de sistema do Windows.     
 
###  <a name="Sort_Order_Defn"></a> Sort Order    
 A ordem de classificação especifica como os valores de dados são classificados. Isso afeta os resultados da comparação de dados. Os dados são classificados com o uso de ordenações e podem ser otimizados com o uso de índices.    
    
##  <a name="Unicode_Defn"></a> Suporte de Unicode    
O Unicode é um padrão para mapear pontos de código para caracteres. Como é projetado para abranger todos os caracteres de todos os idiomas do mundo, não necessita de páginas de código diferentes para lidar com os diferentes conjuntos de caracteres. 
   
As páginas de código usadas por um cliente são determinadas pelas configurações do sistema operacional. Para definir páginas de código de cliente no sistema operacional Windows, use **Configurações Regionais** no Painel de Controle.    

Limitações consideráveis estão associadas a tipos de dados não Unicode. Isso ocorre porque um computador não Unicode fica limitado a usar uma única página de código. Você pode experimentar ganho de desempenho com o uso de Unicode, porque menos conversões de página de código são necessárias. As ordenações Unicode devem ser selecionadas individualmente no nível de banco de dados, coluna ou expressão porque não têm suporte no nível de servidor.    
   
Quando você move dados de um servidor para um cliente, a ordenação do servidor pode não ser reconhecida por drivers de cliente mais antigos. Isso pode ocorrer quando você move dados de um servidor Unicode para um cliente não Unicode. A melhor opção pode ser atualizar o sistema operacional do cliente para que as ordenações de sistema subjacentes sejam atualizadas. Se houver um software de cliente de banco de dados instalado no cliente, você deverá considerar a possibilidade de aplicar uma atualização de serviço a esse software.    
    
> [!TIP]
> Você também pode tentar usar uma ordenação diferente para os dados no servidor. Escolha uma ordenação que mapeia para uma página de código no cliente.    

Se você armazenar dados de caracteres que refletem vários idiomas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), use tipos de dados Unicode (**nchar**, **nvarchar** e **ntext**) em vez de tipos de dados não Unicode (**char**, **varchar** e **text**). 

> [!NOTE]
> No caso dos tipos de dados Unicode, o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] poderá representar até 65.535 caracteres usando o UCS-2 ou o intervalo completo de Unicode (1.114.111 caracteres) se caracteres suplementares forem usados. Para saber mais sobre como habilitar caracteres suplementares, confira o tópico [Caracteres Suplementares](#Supplementary_Characters).

Como alternativa, começando com o [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)], se uma ordenação habilitada para UTF-8 (\_UTF8) for usada, tipos de dados que eram não Unicode (**char** e **varchar**) se tornarão tipos de dados Unicode (UTF-8). O [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] não altera o comportamento de tipos de dados Unicode existentes anteriormente (UTF-16) (**nchar**, **nvarchar** e **ntext**). Para ver mais detalhes, confira [Diferenças de armazenamento entre UTF-8 e UTF-16](#storage_differences).
       
Para usar as ordenações UTF-16 disponíveis no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) para melhorar a pesquisa e classificação de alguns caracteres Unicode (somente ordenações do Windows), selecione uma das ordenações dos caracteres suplementares (\_SC) ou uma das ordenações da versão 140.    
 
Para usar as ordenações UTF-8 disponíveis no [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] para aprimorar a pesquisa e a classificação de alguns caracteres Unicode (somente ordenações do Windows), você precisa selecionar ordenações habilitadas para codificação UTF-8 (\_UTF8).
 
-   O sinalizador de UTF8 pode ser aplicado a:    
    -   Ordenações da versão 90 
        > [!NOTE]
        > Somente quando caracteres suplementares (\_SC) ou ordenações com diferenciação de seletor de variação (\_VSS) já existem nesta versão.
    -   Ordenações da versão 100    
    -   Ordenações da versão 140   
    -   Ordenação binária BIN2<sup>1</sup>
    
-   O sinalizador de UTF8 não pode ser aplicado a:    
    -   Ordenações da versão 90 sem suporte a caracteres suplementares (\_SC) ou a diferenciação de seletor de variação (\_VSS)    
    -   As ordenações primárias BIN ou BIN2<sup>2</sup>    
    -   As ordenações do SQL\*  
    
<sup>1</sup> No [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.3 em diante. O [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 3.0 substituiu a ordenação UTF8_BIN2 pela Latin1_General_100_BIN2_UTF8.     
<sup>2</sup> Até com o [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.3. 
    
Para avaliar os problemas relacionados ao uso de tipos de dados Unicode ou não Unicode, teste seu cenário para medir as diferenças de desempenho em seu ambiente. Uma boa prática é padronizar a ordenação usada nos sistemas de sua organização e implantar servidores e clientes Unicode sempre que possível.    
    
Na maioria das situações, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interage com outros servidores ou clientes, e sua organização poderá usar vários padrões de acesso a dados entre aplicativos e instâncias de servidor. Clientes[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são de um destes dois tipos principais:    
    
-   **Clientes Unicode** que usam OLE DB e ODBC (Open Database Connectivity) versão 3.7 ou uma versão posterior.    
-   **Clientes não Unicode** que usam DB-Library e ODBC versão 3.6 ou uma versão anterior.    
    
A tabela a seguir fornece informações sobre como usar dados multilíngues com várias combinações de servidores Unicode e não Unicode.    
    
|Servidor|Cliente|Benefícios ou limitações|    
|------------|------------|-----------------------------|    
|Unicode|Unicode|Como os dados Unicode são usados em todo o sistema, este cenário fornece o melhor desempenho e proteção contra danos de dados recuperados. É isso o que acontece com ADO (ActiveX Data Objects), OLE DB e ODBC versão 3.7 ou uma versão posterior.|    
|Unicode|Não Unicode|Neste cenário, principalmente em conexões entre um servidor que executa um sistema operacional mais recente e um cliente com uma versão mais antiga do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ou em um sistema operacional mais antigo, pode haver limitações ou erros quando você move os dados para um computador cliente. Os dados Unicode no servidor tentam mapear para uma página de código correspondente no cliente não Unicode para converter os dados.|    
|Não Unicode|Unicode|Esta não é uma configuração ideal para usar dados multilíngues. Não é possível gravar dados Unicode no servidor não Unicode. É provável que ocorram problemas quando os dados forem enviados para servidores que estejam fora da página de código do servidor.|    
|Não Unicode|Não Unicode|Este é um cenário muito limitado para dados multilíngues. Você pode usar uma única página de código.|    
    
##  <a name="Supplementary_Characters"></a> Caracteres complementares    
O Unicode Consortium aloca um ponto de código exclusivo para cada caractere, que é um valor no intervalo de 000000 a 10FFFF. Os caracteres usados com mais frequência têm valores de ponto de código no intervalo de 000000 a 00FFFF (65.535 caracteres) que se encaixam em uma palavra de 8 ou 16 bits na memória e no disco. Geralmente, esse intervalo é designado como BMP (Plano Multilíngue Básico). 

No entanto, o Consortium Unicode estabeleceu 16 "planos" adicionais de caracteres, cada um com o mesmo tamanho do BMP. Com essa definição, o Unicode tem potencial para representar 1.114.112 caracteres (ou seja, 2<sup>16</sup> * 17 caracteres), dentro do intervalo de pontos de código de 000000 a 10FFFF. Os caracteres com valores de ponto de código superiores a 00FFFF exigem duas a quatro palavras consecutivas de 8 bits (UTF-8) ou duas palavras consecutivas de 16 bits (UTF-16). Esses caracteres localizados além do BMP são chamados de *caracteres suplementares*, e as palavras adicionais consecutivas de 8 ou 16 bits são chamadas de *pares alternativos*. Para ver mais detalhes sobre caracteres suplementares, substitutos e pares alternativos, confira o [Padrão Unicode](http://www.unicode.org/standard/standard.html).    

O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece tipos de dados, como **nchar** e **nvarchar**, para armazenar dados Unicode no intervalo do BMP (000000 a 00FFFF), que o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] codifica com UCS-2. 

O [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] adicionou uma nova família de ordenações de caracteres suplementares (\_SC) que podem ser usados com os tipos de dados **nchar**, **nvarchar** e **sql_variant** para representar o intervalo completo de caracteres Unicode (000000 a 10FFFF). Por exemplo: `Latin1_General_100_CI_AS_SC` ou, ao usar uma ordenação de japonês, `Japanese_Bushu_Kakusu_100_CI_AS_SC`. 
 
O [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] estende o suporte a caracteres suplementares para os tipos de dados **char** e **varchar** com as novas ordenações habilitadas para UTF-8 ([\_UTF8](#utf8)). Elas também podem representar o intervalo completo de caracteres Unicode.   

> [!NOTE]
> A partir do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], todas as novas ordenações da versão **\_140** são automaticamente compatíveis com caracteres suplementares.

Se você usar caracteres suplementares:    
    
-   Caracteres suplementares podem ser usados apenas em operações de comparação e ordenação em versões de ordenação 90 ou superior.    
-   Todas as ordenações de versão 100 dão suporte à classificação linguística com caracteres suplementares.    
-   Os caracteres suplementares não têm suporte para uso em metadados, como em nomes de objetos de banco de dados.    
-   Bancos de dados que usam ordenações com caracteres suplementares (\_SC), não podem ser habilitados para replicação de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Isso ocorre porque alguns dos procedimentos armazenados e tabelas do sistema criados para replicação usam o tipo de dados **ntext** herdado que não é compatível com caracteres suplementares.  

-   O sinalizador de SC pode ser aplicado a:    
    -   Ordenações da versão 90    
    -   Ordenações da versão 100    
    
-   O sinalizador de SC não pode ser aplicado a:    
    -   Ordenações do Windows sem versão na versão 80    
    -   As ordenações primárias BIN ou BIN2    
    -   As ordenações do SQL\*    
    -   Ordenações da versão 140 (eles não precisam do sinalizador de SC pois já dão suporte a caracteres suplementares)    
    
A seguinte tabela compara o comportamento de alguns operadores e funções de cadeia de caracteres quando eles usam caracteres suplementares com e sem uma ordenação SCA (reconhecimento de caracteres suplementares):    
    
|Função ou operador de cadeia de caracteres|Com uma ordenação SCA (Reconhecimento de Caracteres Suplementares)|Sem uma ordenação de SCA|    
|---------------------------------|--------------------------|-----------------------------|    
|[CHARINDEX](../../t-sql/functions/charindex-transact-sql.md)<br /><br /> [LEN](../../t-sql/functions/len-transact-sql.md)<br /><br /> [PATINDEX](../../t-sql/functions/patindex-transact-sql.md)|O par substituto UTF-16 é contado como um único ponto de código.|O par substituto UTF-16 é contado como dois pontos de código.|    
|[LEFT](../../t-sql/functions/left-transact-sql.md)<br /><br /> [REPLACE](../../t-sql/functions/replace-transact-sql.md)<br /><br /> [REVERSE](../../t-sql/functions/reverse-transact-sql.md)<br /><br /> [RIGHT](../../t-sql/functions/right-transact-sql.md)<br /><br /> [SUBSTRING](../../t-sql/functions/substring-transact-sql.md)<br /><br /> [STUFF](../../t-sql/functions/stuff-transact-sql.md)|Essas funções tratam cada par substituto como um único ponto de código e funcionam conforme o esperado.|Essas funções podem dividir qualquer par substituto e levar a resultados inesperados.|    
|[NCHAR](../../t-sql/functions/nchar-transact-sql.md)|Retorna o caractere que corresponde ao valor de ponto de código Unicode especificado no intervalo de 0 a 0x10FFFF. Se o valor especificado estiver no intervalo de 0 a 0xFFFF, será retornado um caractere. Para valores mais altos, é retornado o substituto correspondente.|Um valor mais alto que 0xFFFF retorna NULL, em vez do substituto correspondente.|    
|[UNICODE](../../t-sql/functions/unicode-transact-sql.md)|Retorna um ponto de código UTF-16 no intervalo de 0 a 0x10FFFF.|Retorna um ponto de código UCS-2 no intervalo de 0 a 0xFFFF.|    
|[Corresponder a um caractere curinga](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)<br /><br /> [Curinga – caracter(es) para não corresponder](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)|Há suporte para caracteres suplementares para todas as operações de curingas.|Não há suporte para caracteres suplementares para estas operações de curingas. Há suporte para outros operadores curinga.|    
    
## <a name="GB18030"></a> Suporte a GB18030    
GB18030 é um padrão separado usado na República Popular da China para codificar caracteres chineses. Em GB18030, caracteres podem ter 1, 2 ou 4 bytes em comprimento. O[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte a caracteres GB18030 codificados, reconhecendo-os quando eles entram no servidor, provenientes de um aplicativo cliente, convertendo-os e armazenando-os nativamente como caracteres Unicode. Após serem armazenados no servidor, são tratados como caracteres Unicode em todas as operações subsequentes. Você pode usar qualquer ordenação em chinês, preferivelmente a mais recente versão 100. Todas as ordenações de nível _100 dão suporte à classificação linguística com caracteres GB18030. Se os dados incluírem caracteres suplementares (pares alternativos), você poderá usar as ordenações de SC disponíveis no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para aprimorar a pesquisa e a classificação.    
    
## <a name="Complex_script"></a> Suporte a script complexo    
O[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte à inserção, armazenamento, alteração e exibição de scripts complexos. Scripts complexos incluem os seguintes tipos:    
    
-   Scripts que incluem uma combinação de texto da direita para a esquerda e da esquerda para a direita, como uma combinação de texto em árabe e inglês.    
-   Scripts cujos caracteres alteram de forma de acordo com sua posição ou quando combinados com outros caracteres, como caracteres árabes, índicos e tailandeses.    
-   Idiomas como tailandês que exigem dicionários internos reconhecer palavras porque não há nenhuma quebra entre eles.    
    
Aplicativos de banco de dados que interagem com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devem usar controles que oferecem suporte a scripts complexos. Controles de formulário padrão do Windows que são criados em código gerenciado são habilitados para script complexo.    

## <a name="Japanese_Collations"></a> Ordenações em japonês adicionados no  [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]
 
A partir do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)], há suporte para novas famílias de ordenação em japonês, com as permutações de várias opções (\_CS, \_AS, \_KS, \_WS, \_VSS). 

Para listar essas ordenações, você pode consultar o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]:      

```sql 
SELECT Name, Description FROM fn_helpcollations()  
WHERE Name LIKE 'Japanese_Bushu_Kakusu_140%' OR Name LIKE 'Japanese_XJIS_140%'
``` 

Todas as novas ordenações têm suporte interno para caracteres suplementares, de modo que nenhuma das novas ordenações da versão **\_140** têm (ou precisa de) sinalizador de SC.

Essas ordenações são compatíveis com índices, tabelas com otimização de memória, índices columnstore e módulos compilados nativamente no [!INCLUDE[ssde_md](../../includes/ssde_md.md)].

<a name="ctp23"></a>

## <a name="utf8"></a> Suporte para UTF-8
O [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] apresenta suporte completo para a codificação de caracteres UTF-8 amplamente utilizada como codificação de importação ou exportação e como ordenação em nível de coluna ou de banco de dados para dados de cadeia de caracteres. A UTF-8 é permitida nos tipos de dados **char** e **varchar** e é habilitada quando você cria ou altera a ordenação de um objeto para uma ordenação com o sufixo `UTF8`. Por exemplo, `LATIN1_GENERAL_100_CI_AS_SC` para `LATIN1_GENERAL_100_CI_AS_SC_UTF8`. 

A UTF-8 só está disponível para ordenações do Windows com suporte para caracteres suplementares, conforme introduzida no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Os tipos de dados **nchar** e **nvarchar** permitem apenas codificação UCS-2 e UTF-16 e permanecem inalterados.

### <a name="storage_differences"></a> Diferenças de armazenamento entre UTF-8 e UTF-16
O Unicode Consortium aloca um ponto de código exclusivo para cada caractere, que é um valor no intervalo de 000000 a 10FFFF. Com o [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)], as codificações em UTF-8 e UTF-16 estão disponíveis para representar o intervalo completo:    
-  Com a codificação UTF-8, os caracteres no intervalo de ASCII (000000 – 00007F) exigem 1 byte, os pontos de código de 000080 a 0007FF exigem 2 bytes, os pontos de código de 000800 a 00FFFF exigem 3 bytes e os pontos de código de 0010000 a 0010FFFF exigem 4 bytes. 
-  Com a codificação UTF-16, os pontos de código de 000000 a 00FFFF exigem 2 bytes e os pontos de código de 0010000 a 0010FFFF exigem 4 bytes. 

A tabela a seguir descreve os bytes de armazenamento de codificação para cada intervalo de caracteres e tipo de codificação:

|Intervalo de códigos (hexadecimal)|Intervalo de códigos (decimal)|Bytes de armazenamento <sup>1</sup> com UTF-8|Bytes de armazenamento <sup>1</sup> com UTF-16|    
|---------------------------------|---------------------------------|--------------------------|-----------------------------|   
|000000 – 00007F|0 – 127|1|2|
|000080 – 00009F<br />0000A0 – 0003FF<br />000400 – 0007FF|128 – 159<br />160 – 1.023<br />1\.024 – 2.047|2|2|
|000800 – 003FFF<br />004000 – 00FFFF|2\.048 – 16.383<br />16.384 – 65.535|3|2|
|010000 – 03FFFF <sup>2</sup><br /><br />040000 – 10FFFF <sup>2</sup>|65.536 – 262.143 <sup>2</sup><br /><br />262.144 – 1.114.111 <sup>2</sup>|4|4|

<sup>1</sup> Os bytes de armazenamento se referem ao comprimento do byte codificado, e não ao tamanho de armazenamento em disco do respectivo tipo de dados. Para saber mais sobre tamanhos de armazenamento em disco, confira os tipos de dados [nchar e nvarchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md) e [char e varchar](../../t-sql/data-types/char-and-varchar-transact-sql.md).

<sup>2</sup> Intervalo de pontos de código para [caracteres suplementares](#Supplementary_Characters).

> [!TIP]   
> É comum pensar em [CHAR(*n*) e em VARCHAR(*n*)](../../t-sql/data-types/char-and-varchar-transact-sql.md) ou em [NCHAR(*n*) e em NVARCHAR(*n*)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md), o *n* define o número de caracteres. Isso ocorre porque, no exemplo de uma coluna CHAR(10), 10 caracteres ASCII no intervalo 0-127 podem ser armazenados usando uma ordenação como Latin1_General_100_CI_AI, porque cada caractere nesse intervalo usa apenas 1 byte.    
> No entanto, em [CHAR(*n*) e em VARCHAR(*n*)](../../t-sql/data-types/char-and-varchar-transact-sql.md), o *n* define o tamanho da cadeia de caracteres em **bytes** (0-8.000), enquanto em [NCHAR(*n*) e em NVARCHAR(*n*)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md) o *n* define o tamanho da cadeia de caracteres em **pares de bytes** (0-4.000). *n* nunca define números de caracteres que podem ser armazenados.

Como descrito acima, a escolha da codificação e do tipo de dados Unicode apropriados pode proporcionar economias significativas de armazenamento ou aumentar o volume de armazenamento atual, dependendo do conjunto de caracteres em uso. Por exemplo, ao usar uma ordenação Latin que é habilitada para UTF-8, como Latin1_General_100_CI_AI_SC_UTF8, uma coluna `CHAR(10)` armazena 10 bytes e pode conter 10 caracteres ASCII no intervalo 0-127, mas apenas cinco caracteres no intervalo 128-2047 e apenas três caracteres no intervalo 2048-65535. Por comparação, como uma coluna `NCHAR(10)` armazena 10 pares de bytes (20 bytes), ela pode conter 10 caracteres no intervalo de 0-65535.  

Antes de usar a codificação UTF-8 ou UTF-16 para um banco de dados ou uma coluna, considere a distribuição dos dados de cadeia de caracteres que serão armazenados:
-  Se a maioria estiver no intervalo 0-127 de ASCII (como o idioma inglês), cada caractere exigirá 1 byte com UTF-8 e 2 bytes com UTF-16. O uso de UTF-8 proporciona vantagens de armazenamento. A alteração de um tipo de dados de coluna existente com caracteres ASCII no intervalo 0-127 de `NCHAR(10)` a `CHAR(10)` usando uma ordenação habilitada para UTF-8 converte 50 por cento de redução em requisitos de armazenamento. Essa redução ocorre porque `NCHAR(10)` exige 20 bytes para armazenamento, enquanto `CHAR(10)` exige 10 bytes para a mesma representação de cadeia de caracteres Unicode.    
-  Acima do intervalo de ASCII, quase todos os scripts latinos, além de árabe, armênio, cirílico, copta, grego, hebraico, n’ko, siríaco e tāna exigirão 2 bytes por caractere em UTF-8 e UTF-16. Nesses casos, não há diferenças significativas de armazenamento para tipos de dados comparáveis (por exemplo, entre o uso dos tipos de dados **char** ou **nchar**).
-  Se a maioria for de scripts do Leste Asiático (como chinês, coreano e japonês), cada caractere exigirá 3 bytes com UTF-8 e 2 bytes com UTF-16. O uso de UTF-16 proporciona vantagens de armazenamento. 
-  Os caracteres no intervalo de 010000 a 10FFFF exigem 4 bytes tanto em UTF-8 como em UTF-16. Nesses casos, não há diferenças de armazenamento para tipos de dados comparáveis (por exemplo, entre o uso dos tipos de dados **char** ou **nchar**).

Para ver outras considerações, confira o artigo [Gravar instruções Transact-SQL internacionais](../../relational-databases/collations/write-international-transact-sql-statements.md).

##  <a name="Related_Tasks"></a> Tarefas relacionadas    
    
|Tarefa|Tópico|    
|----------|-----------|    
|Descreve como definir ou alterar a ordenação da instância de SQL Server.|[Definir ou alterar a ordenação do servidor](../../relational-databases/collations/set-or-change-the-server-collation.md)|    
|Descreve como definir ou alterar a ordenação de um banco de dados de usuário.|[Definir ou alterar a ordenação de banco de dados](../../relational-databases/collations/set-or-change-the-database-collation.md)|    
|Descreve como definir ou alterar a ordenação de uma coluna no banco de dados.|[Definir ou alterar a ordenação de coluna](../../relational-databases/collations/set-or-change-the-column-collation.md)|    
|Descreve como retornar informações de ordenação ao servidor, banco de dados ou nível de coluna.|[Exibir informações de ordenação](../../relational-databases/collations/view-collation-information.md)|    
|Descreve como escrever instruções Transact-SQL que tenham mais portabilidade de um idioma para outro ou que ofereçam suporte a vários idiomas mais facilmente.|[Gravar instruções Transact-SQL internacionais](../../relational-databases/collations/write-international-transact-sql-statements.md)|    
|Descreve como alterar o idioma de mensagens de erro e preferências de como data, hora e dados de moeda são usados e exibidos.|[Definir um idioma de sessão](../../relational-databases/collations/set-a-session-language.md)|    
    
##  <a name="Related_Content"></a> Conteúdo relacionado    
[Práticas recomendadas para alteração em ordenações do SQL Server](https://go.microsoft.com/fwlink/?LinkId=113891)    
[Usar o formato de caractere Unicode para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)        
[Gravar instruções Transact-SQL internacionais](../../relational-databases/collations/write-international-transact-sql-statements.md)     
["Práticas recomendadas para migração para Unicode no SQL Server"](https://go.microsoft.com/fwlink/?LinkId=113890) – deixou de receber manutenção   
[Site do Unicode Consortium](https://go.microsoft.com/fwlink/?LinkId=48619)   
[Padrão Unicode](http://www.unicode.org/standard/standard.html)     
[Suporte ao UTF-8 no OLE DB Driver for SQL Server](../../connect/oledb/features/utf-8-support-in-oledb-driver-for-sql-server.md)  
Blog [Apresentação do suporte a UTF-8 para SQL Server](https://techcommunity.microsoft.com/t5/SQL-Server/Introducing-UTF-8-support-for-SQL-Server/ba-p/734928)       
    
## <a name="see-also"></a>Consulte Também    
[Ordenações de banco de dados independentes](../../relational-databases/databases/contained-database-collations.md)     
[Escolher um idioma ao criar um índice de texto completo](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md)     
[sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)    
    
 
