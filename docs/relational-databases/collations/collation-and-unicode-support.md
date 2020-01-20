---
title: Suporte a ordenações e Unicode | Microsoft Docs
ms.custom: ''
ms.date: 12/05/2019
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
author: pmasl
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2d20f0cd4a08e22787caecfb663ef0d2dcd47003
ms.sourcegitcommit: 365a919e3f0b0c14440522e950b57a109c00a249
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/10/2020
ms.locfileid: "75831810"
---
# <a name="collation-and-unicode-support"></a>Suporte a ordenações e Unicode
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
As ordenações em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornecem propriedades de regras de classificação, de diferenciação de maiúsculas e minúsculas e de diferenciação de acentos para seus dados. As ordenações usadas com tipos de dados de caractere, como **char** e **varchar**, determinam a página de código e os caracteres correspondentes que podem ser representados para esse tipo de dados. 

Independentemente de você estar instalando uma nova instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], restaurando um backup de banco de dados ou conectando o servidor a bancos de dados cliente, é importante estar ciente dos requisitos de localidade, da ordem de classificação e da diferenciação de maiúsculas e minúsculas e de acentos dos dados com os quais você está trabalhando. Para listar as ordenações disponíveis na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], confira [sys.fn_helpcollations (Transact-SQL)](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md).    
    
Ao selecionar uma ordenação para o servidor, o banco de dados, a coluna ou a expressão, você atribui determinadas características aos dados. Essas características afetam os resultados de muitas operações no banco de dados. Por exemplo, ao construir uma consulta usando `ORDER BY`, a ordem de classificação do conjunto de resultados poderá depender da ordenação aplicada ao banco de dados ou determinada em uma cláusula `COLLATE` no nível de expressão da consulta.    
    
Para usar o suporte a ordenações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da melhor maneira possível, você deve estar ciente dos termos definidos neste tópico e de como eles estão relacionados às características dos dados.    
    
##  <a name="Terms"></a> Termos de ordenação    
    
-   [Ordenação](#Collation_Defn) 
    - [Conjuntos de ordenações](#Collation_sets)
    - [Níveis de ordenação](#Collation_levels)
-   [Localidade](#Locale_Defn)    
-   [Página de código](#Code_Page_Defn)    
-   [Ordem de classificação](#Sort_Order_Defn)    
    
###  <a name="Collation_Defn"></a> Ordenação    
Uma ordenação especifica os padrões de bit que representam cada caractere em um conjunto de dados. As ordenações também determinam as regras que classificam e comparam dados. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte ao armazenamento de objetos com ordenações diferentes em um banco de dados individual. Para colunas não Unicode, a configuração de ordenação especifica a página de códigos dos dados e quais caracteres podem ser representados. Os dados movidos entre colunas não Unicode precisam ser convertidos da página de código de origem para a página de código de destino.    
    
Os resultados da instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] podem variar quando a instrução for executada no contexto de diferentes bancos de dados que tenham configurações de ordenação diferentes. Se possível, use uma ordenação padronizada para sua organização. Desse modo, não será preciso especificar a ordenação em cada caractere ou expressão Unicode. Se você deve trabalhar com objetos que tenham configurações de ordenação e página de códigos diferentes, codifique suas consultas para considerar as regras da precedência de ordenação. Para obter mais informações, consulte [Precedência de ordenação (Transact-SQL)](../../t-sql/statements/collation-precedence-transact-sql.md).    
    
As opções associadas a uma ordenação são diferenciação de maiúsculas e minúsculas, de acentos, de caracteres Kana, de largura e de seletor de variação. O [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] introduz uma opção adicional para codificação [UTF-8](https://www.wikipedia.org/wiki/UTF-8). 

Especifique essas opções acrescentando-as ao nome da ordenação. Por exemplo, a ordenação **Japanese_Bushu_Kakusu_100_CS_AS_KS_WS_UTF8** diferencia maiúsculas de minúsculas, acentos, caracteres Kana, a largura e é codificado em UTF-8. Como outro exemplo, a ordenação **Japanese_Bushu_Kakusu_140_CI_AI_KS_WS_VSS** não diferencia maiúsculas de minúsculas, não diferencia acentos, mas diferencia caracteres Kana, a largura e o seletor de variação, além de usar a codificação não Unicode. 

O comportamento associado a essas várias opções é descrito na seguinte tabela:    
    
|Opção|Descrição|    
|------------|-----------------|    
|Diferenciar maiúsculas de minúsculas (\_CS)|Faz distinção entre letras maiúscula e minúsculas. Se essa opção for selecionada, as letras minúsculas serão classificadas à frente das versões em letras maiúsculas. Se essa opção não for selecionada, a ordenação não diferenciará maiúsculas de minúsculas. Ou seja, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considera as versões de letras maiúsculas e minúsculas como idênticas para fins de classificação. Você pode selecionar explicitamente a não diferenciação de maiúsculas e minúsculas, especificando \_CI.|   
|Diferenciar acentos (\_AS)|Faz distinção entre caracteres acentuados e não acentuados. Por exemplo, "a" não é igual a "ấ". Se essa opção não for selecionada, a ordenação não diferenciará acentos. Ou seja, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considera as versões com e sem acentos como idênticas para fins de classificação. Você pode selecionar explicitamente a não diferenciação de acentos, especificando \_AI.|    
|Diferenciar caracteres Kana (\_KS)|Distingue entre os dois tipos de caracteres kana japoneses: hiragana e katakana. Se essa opção não for selecionada, a ordenação não diferenciará caracteres Kana. Ou seja, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considera que caracteres hiragana e katakana são iguais para fins de classificação. A omissão dessa opção é o único método de especificar a não diferenciação de caracteres Kana.|   
|Diferenciar largura (\_WS)|Faz distinção entre caracteres de largura inteira e de meia largura. Se essa opção não for selecionada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considerará as representações de largura inteira e de meia largura do mesmo caractere como idênticas para fins de classificação. A omissão desta opção é o único método de especificar a não diferenciação de largura.|  
|Distinção de seletor de variação (\_VSS)|Distingue entre vários seletores de variação de ideograma nas ordenações de japonês **Japanese_Bushu_Kakusu_140** e **Japanese_XJIS_140**, introduzidas no [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]. Uma sequência de variação consiste em um caractere base e um seletor de variação adicional. Se essa opção \_VSS não for selecionada, a ordenação não diferenciará o seletor de variação e o seletor de variação não será considerado na comparação. Ou seja, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considera caracteres que seguem o mesmo caractere base com seletores de variação distintos como sendo idênticos para fins de classificação. Para obter mais informações, confira [Banco de dados de variação de ideograma Unicode](https://www.unicode.org/reports/tr37/).<br/><br/> Não há suporte para ordenações \_VSS (diferenciação do seletor de variação) em índices de pesquisa de texto completo. Índices de pesquisa de texto completo dão suporte apenas às opções Diferenciação de Acentos (\_AS), Diferenciação de caracteres Kana (\_KS) e Diferenciação de largura (\_WS). Os mecanismos de XML e CLR do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não dão suporte a seletores de variação (\_VSS).|      
|Binário (\_BIN)<sup>1</sup>|Classifica e compara dados em tabelas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com base nos padrões de bit definidos para cada caractere. A ordem de classificação binária faz distinção entre maiúsculas e minúsculas e acentuação. Binário é também a ordem de classificação mais rápida. Para obter mais informações, confira a seção [Ordenações primárias](#Binary-collations) neste artigo.|      
|Ponto de código binário (\_BIN2)<sup>1</sup> | Classifica e compara dados em tabelas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com base em pontos de código Unicode para dados Unicode. Para dados não Unicode, o ponto de código binário usa comparações que são idênticas àquelas das classificações binárias.<br/><br/> A vantagem de usar uma ordem de classificação ponto de código binário é que nenhuma reclassificação de dados será necessária em aplicativos que comparam dados classificados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Como resultado, uma ordem de classificação de ponto de código binário fornece desenvolvimento de aplicativos mais simples e possíveis aumentos de desempenho. Para obter mais informações, confira a seção [Ordenações primárias](#Binary-collations) neste artigo.|
|UTF-8 (\_UTF8)|Permite que dados codificados em UTF-8 sejam armazenados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se essa opção não for selecionada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usará o formato de codificação não Unicode padrão para os tipos de dados aplicáveis. Para obter mais informações, confira a seção [Suporte a UTF-8](#utf8) neste artigo.| 

<sup>1</sup> Se a opção Binário ou Ponto de código binário foi selecionada, as opções Diferenciar maiúsculas de minúsculas (\_CS), Distinguir acentos (\_AS), Distinguir caracteres Kana (\_KS) e Distinguir largura (\_WS) não estarão disponíveis.      

#### <a name="examples-of-collation-options"></a>Exemplos de opções de ordenação
Cada ordenação é combinada como uma série de sufixos para definir a diferenciação de maiúsculas e minúsculas, de acentos, da largura ou de caracteres Kana. Os exemplos a seguir descrevem o comportamento da ordem de classificação para várias combinações de sufixos.

|Sufixo de ordenação do Windows|Descrição da ordem de classificação|
|------------|-----------------| 
|\_BIN<sup>1</sup>|Classificação binária|
|\_BIN2<sup>1, 2</sup>|Ordem de classificação do ponto de código binário|
|\_CI_AI<sup>2</sup>|Não diferencia maiúsculas de minúsculas, acentos, caracteres Kana e a largura|
|\_CI_AI_KS<sup>2</sup>|Não distingue maiúsculas e minúsculas, não distingue acentuação, distingue caracteres kana, não distingue largura|
|\_CI_AI_KS_WS<sup>2</sup>|Não distingue maiúsculas e minúsculas, não distingue acentuação, distingue caracteres kana, distingue largura|
|\_CI_AI_WS<sup>2</sup>|Não distingue maiúsculas e minúsculas, não distingue acentuação, não distingue caracteres kana, distingue largura|
|\_CI_AS<sup>2</sup>|Não distingue maiúsculas e minúsculas, distingue acentuação, não distingue caracteres kana, não distingue largura|
|\_CI_AS_KS<sup>2</sup>|Não distingue maiúsculas e minúsculas, distingue acentuação, distingue caracteres kana, não distingue largura|
|\_CI_AS_KS_WS<sup>2</sup>|Não distingue maiúsculas e minúsculas, distingue acentuação, distingue caracteres kana, distingue largura|
|\_CI_AS_WS<sup>2</sup>|Não distingue maiúsculas e minúsculas, distingue acentuação, não distingue caracteres kana, distingue largura|
|\_CS_AI<sup>2</sup>|Distingue maiúsculas e minúsculas, não distingue acentuação, não distingue caracteres kana, não distingue largura|
|\_CS_AI_KS<sup>2</sup>|Distingue maiúsculas e minúsculas, não distingue acentuação, distingue caracteres kana, não distingue largura|
|\_CS_AI_KS_WS<sup>2</sup>|Distingue maiúsculas e minúsculas, não distingue acentuação, distingue caracteres kana, distingue largura|
|\_CS_AI_WS<sup>2</sup>|Distingue maiúsculas e minúsculas, não distingue acentuação, não distingue caracteres kana, distingue largura|
|\_CS_AS<sup>2</sup>|Distingue maiúsculas e minúsculas, distingue acentuação, não distingue caracteres kana, não distingue largura|
|\_CS_AS_KS<sup>2</sup>|Distingue maiúsculas e minúsculas, distingue acentuação, distingue caracteres kana, não distingue largura|
|\_CS_AS_KS_WS<sup>2</sup>|Distingue maiúsculas e minúsculas, distingue acentuação, distingue caracteres kana, distingue largura|
|\_CS_AS_WS<sup>2</sup>|Distingue maiúsculas e minúsculas, distingue acentuação, não distingue caracteres kana, distingue largura|

<sup>1</sup> Se Binário ou Ponto de código binário for selecionado, as opções Diferencia maiúsculas de minúsculas (\_CS), Diferencia acentos (\_AS), Diferencia caracteres Kana (\_KS) e Diferencia a largura (\_WS) não estarão disponíveis.    

<sup>2</sup> A adição da opção UTF-8 (\_UTF8) permite que você codifique dados Unicode usando UTF-8. Para obter mais informações, confira a seção [Suporte a UTF-8](#utf8) neste artigo. 

### <a name="Collation_sets"></a> Conjuntos de ordenações

O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte aos seguintes conjuntos de ordenação:    

-  [Ordenações do Windows](#Windows-collations)
-  [Ordenações primárias](#Binary-collations)
-  [Ordenações do SQL Server](#SQL-collations)
    
#### <a name="Windows-collations"></a> Ordenações do Windows    
As ordenações do Windows definem regras para o armazenamento de dados de caractere baseados em uma localidade associada do sistema do Windows. No caso de uma ordenação do Windows, você pode implementar uma comparação de dados não Unicode usando o mesmo algoritmo dos dados Unicode. As regras de base da ordenação do Windows especificam qual alfabeto ou idioma é usado quando a classificação do dicionário é aplicada. As regras também especificam a página de código usada para armazenar dados de caractere não Unicode. As classificações Unicode e não Unicode são compatíveis com comparações de cadeias de caracteres em uma versão específica do Windows. Isso proporciona consistência entre os tipos de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e permite que os desenvolvedores classifiquem as cadeias de caracteres nos aplicativos usando as mesmas regras utilizadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, confira [Nome de ordenação do Windows (Transact-SQL)](../../t-sql/statements/windows-collation-name-transact-sql.md).    
    
#### <a name="Binary-collations"></a> Ordenações primárias    
Os dados classificados de ordenações primárias na sequência de valores codificados definidos pelo tipo de localidade e dados. Eles diferenciam maiúsculas de minúsculas. Uma ordenação primária no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] define a localidade e a página de código ANSI que são usadas. Isso impõe uma ordem de classificação binária. Como são relativamente simples, as ordenações primárias ajudam melhorar o desempenho do aplicativo. Para tipos de dados não Unicode, as comparações de dados têm como base os pontos de código definidos na página de código ANSI. Para tipos de dados Unicode, as comparações de dados têm como base os pontos de código Unicode. Para ordenações primárias em tipos de dados Unicode, a localidade não é considerada nas classificações de dados. Por exemplo, **Latin_1_General_BIN** e **Japanese_BIN** geram resultados de classificação idênticos quando usados em dados Unicode. Para obter mais informações, confira [Nome de ordenação do Windows (Transact-SQL)](../../t-sql/statements/windows-collation-name-transact-sql.md).   
    
Há dois tipos de agrupamentos binários no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:

-  As ordenações **BIN** herdadas, que executavam uma comparação de ponto de código para ponto de código incompleta para dados Unicode. Essas ordenações primárias herdadas comparavam o primeiro caractere como WCHAR, seguido por uma comparação byte por byte. Em uma ordenação BIN, apenas o primeiro caractere é classificado de acordo com o ponto de código e os caracteres restantes são classificados de acordo com os respectivos valores de bytes.

-  As ordenações **BIN2** mais recentes, que implementam uma comparação de ponto de código puro. Em uma ordenação BIN2, todos os caracteres são classificados de acordo com os respectivos pontos de código. Já que a plataforma Intel é um arquitetura little endian, os caracteres de código Unicode são sempre trocados por bytes armazenados.     
    
#### <a name="SQL-collations"></a> Ordenações do SQL Server    
As ordenações (SQL_\*) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferecem compatibilidade de ordem de classificação com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. As regras de classificação do dicionário para dados não Unicode são incompatíveis com as rotinas de classificação fornecidas pelos sistemas operacionais Windows. No entanto, a classificação de dados Unicode é compatível com uma versão específica das regras de classificação do Windows. Como as ordenações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usam regras de comparação diferentes para dados não Unicode e Unicode, você vê resultados diferentes para comparações dos mesmos dados, dependendo do tipo de dados subjacente. Para obter mais informações, confira [Nome de ordenação do SQL Server (Transact-SQL)](../../t-sql/statements/sql-server-collation-name-transact-sql.md). 

Durante a instalação de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a instalação de ordenação padrão é determinada pela localidade do SO (sistema operacional). Você pode alterar a ordenação no nível de servidor durante a instalação ou por meio da alteração da localidade do sistema operacional antes da instalação. Por motivos de compatibilidade com versões anteriores, a ordenação padrão é definida como a versão disponível mais antiga associada a cada localidade específica. Portanto, essa nem sempre é a ordenação recomendada. Para aproveitar ao máximo os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], altere as configurações de instalação padrão para usar ordenações do Windows. Por exemplo, para a localidade do sistema operacional "Inglês (Estados Unidos)" (página de código 1252), a ordenação padrão durante a instalação é **SQL_Latin1_General_CP1_CI_AS**, que pode ser alterada para a ordenação equivalente do Windows mais próxima, **Latin1_General_100_CI_AS_SC**.
    
> [!NOTE]    
> Ao atualizar uma instância em inglês do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode especificar ordenações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQL_\*) para compatibilidade com as instâncias existentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Como a ordenação padrão de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é definida durante a instalação, lembre-se de especificar as configurações de ordenação com cuidado quando as seguintes condições forem verdadeiras:    
>     
> -   Seu código de aplicativo depende do comportamento de ordenações anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].    
> -   Você deve armazenar dados de caractere que refletem vários idiomas.    
    
### <a name="Collation_levels"></a> Níveis de ordenação
Há suporte para configurar ordenações nos seguintes níveis de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:    

-  [Ordenações no nível do servidor](#Server-level-collations)
-  [Ordenações do nível do banco de dados](#Database-level-collations)
-  [Ordenações em nível de coluna](#Column-level-collations)
-  [Ordenações no nível da expressão](#Expression-level-collations)

#### <a name="Server-level-collations"></a> Ordenações no nível do servidor   
A ordenação do servidor padrão é determinada durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e se torna a ordenação padrão dos bancos de dados do sistema e de todos os bancos de dados de usuário. 

A seguinte tabela mostra as designações de ordenação padrão conforme determinado pela localidade do sistema operacional, incluindo os respectivos LCIDs (identificadores de código de idioma) do Windows e do SQL:

|Localidade do Windows|LCID do Windows|LCID do SQL|Ordenação padrão|
|---------------|---------|---------|---------------|
|Africâner (África do Sul)|0x0436|0x0409|Latin1_General_CI_AS|
|Albanês (Albânia)|0x041c|0x041c|Albanian_CI_AS|
|Alsaciano (França)|0x0484|0x0409|Latin1_General_CI_AS|
|Amárico (Etiópia)|0x045e|0x0409|Latin1_General_CI_AS|
|Árabe (Argélia)|0x1401|0x0401|Arabic_CI_AS|
|Árabe (Bahrein)|0x3c01|0x0401|Arabic_CI_AS|
|Árabe (Egito)|0x0c01|0x0401|Arabic_CI_AS|
|Árabe (Iraque)|0x0801|0x0401|Arabic_CI_AS|
|Árabe (Jordânia)|0x2c01|0x0401|Arabic_CI_AS|
|Árabe (Kuwait)|0x3401|0x0401|Arabic_CI_AS|
|Árabe (Líbano)|0x3001|0x0401|Arabic_CI_AS|
|Árabe (Líbia)|0x1001|0x0401|Arabic_CI_AS|
|Árabe (Marrocos)|0x1801|0x0401|Arabic_CI_AS|
|Árabe (Omã)|0x2001|0x0401|Arabic_CI_AS|
|Árabe (Catar)|0x4001|0x0401|Arabic_CI_AS|
|Árabe (Arábia Saudita)|0x0401|0x0401|Arabic_CI_AS|
|Árabe (Síria)|0x2801|0x0401|Arabic_CI_AS|
|Árabe (Tunísia)|0x1c01|0x0401|Arabic_CI_AS|
|Árabe (EAU)|0x3801|0x0401|Arabic_CI_AS|
|Árabe (Iêmen)|0x2401|0x0401|Arabic_CI_AS|
|Armênio (Armênia)|0x042b|0x0419|Latin1_General_CI_AS|
|Assamês (Índia)|0x044d|0x044d|Indisponível no nível do servidor|
|Azeri (Azerbaijão, cirílico)|0x082c|0x082c|Preterido, não disponível no nível do servidor|
|Azeri (Azerbaijão, latino)|0x042c|0x042c|Preterido, não disponível no nível do servidor|
|Bashkir (Rússia)|0x046d|0x046d|Latin1_General_CI_AI|
|Basco (País Basco)|0x042d|0x0409|Latin1_General_CI_AS|
|Bielorrusso (Belarus)|0x0423|0x0419|Cyrillic_General_CI_AS|
|Bengali (Bangladesh)|0x0845|0x0445|Indisponível no nível do servidor|
|Bengali (India)|0x0445|0x0439|Indisponível no nível do servidor|
|Bósnio (Bósnia e Herzegovina, Cirílico)|0x201a|0x201a|Latin1_General_CI_AI|
|Bósnio (Bósnia e Herzegovina, Latino)|0x141a|0x141a|Latin1_General_CI_AI|
|Bretão (França)|0x047e|0x047e|Latin1_General_CI_AI|
|Búlgaro (Bulgária)|0x0402|0x0419|Cyrillic_General_CI_AS|
|Catalão (Catalunha)|0x0403|0x0409|Latin1_General_CI_AS|
|Chinês (RAE de Hong Kong, RPC)|0x0c04|0x0404|Chinese_Taiwan_Stroke_CI_AS|
|Chinese (Macao SAR)|0x1404|0x1404|Latin1_General_CI_AI|
|Chinês (Macau)|0x21404|0x21404|Latin1_General_CI_AI|
|Chinês (China)|0x0804|0x0804|Chinese_PRC_CI_AS|
|Chinês (China)|0x20804|0x20804|Chinese_PRC_Stroke_CI_AS|
|Chinês (Singapura)|0x1004|0x0804|Chinese_PRC_CI_AS|
|Chinês (Singapura)|0x21004|0x20804|Chinese_PRC_Stroke_CI_AS|
|Chinês (Taiwan)|0x30404|0x30404|Chinese_Taiwan_Bopomofo_CI_AS|
|Chinês (Taiwan)|0x0404|0x0404|Chinese_Taiwan_Stroke_CI_AS|
|Corso (França)|0x0483|0x0483|Latin1_General_CI_AI|
|Croata (Bósnia e Herzegovina, Latino)|0x101a|0x041a|Croatian_CI_AS|
|Croata (Croácia)|0x041a|0x041a|Croatian_CI_AS|
|Tcheco (República Tcheca)|0x0405|0x0405|Czech_CI_AS|
|Dinamarquês (Dinamarca)|0x0406|0x0406|Danish_Norwegian_CI_AS|
|Dari (Afeganistão)|0x048c|0x048c|Latin1_General_CI_AI|
|Divehi (Maldivas)|0x0465|0x0465|Indisponível no nível do servidor|
|Holandês (Bélgica)|0x0813|0x0409|Latin1_General_CI_AS|
|Holandês (Países Baixos)|0x0413|0x0409|Latin1_General_CI_AS|
|Inglês (Austrália)|0x0c09|0x0409|Latin1_General_CI_AS|
|Inglês (Belize)|0x2809|0x0409|Latin1_General_CI_AS|
|Inglês (Canadá)|0x1009|0x0409|Latin1_General_CI_AS|
|Inglês (Caribe)|0x2409|0x0409|Latin1_General_CI_AS|
|Inglês (Índia)|0x4009|0x0409|Latin1_General_CI_AS|
|Inglês (Irlanda)|0x1809|0x0409|Latin1_General_CI_AS|
|Inglês (Jamaica)|0x2009|0x0409|Latin1_General_CI_AS|
|Inglês (Malásia)|0x4409|0x0409|Latin1_General_CI_AS|
|Inglês (Nova Zelândia)|0x1409|0x0409|Latin1_General_CI_AS|
|Inglês (Filipinas)|0x3409|0x0409|Latin1_General_CI_AS|
|Inglês (Singapura)|0x4809|0x0409|Latin1_General_CI_AS|
|Inglês (África do Sul)|0x1c09|0x0409|Latin1_General_CI_AS|
|Inglês (Trinidad e Tobago)|0x2c09|0x0409|Latin1_General_CI_AS|
|Inglês (Reino Unido)|0x0809|0x0409|Latin1_General_CI_AS|
|Inglês (Estados Unidos)|0x0409|0x0409|SQL_Latin1_General_CP1_CI_AS|
|Inglês (Zimbábue)|0x3009|0x0409|Latin1_General_CI_AS|
|Estoniano (Estônia)|0x0425|0x0425|Estonian_CI_AS|
|Feroês (Ilhas Faroe)|0x0438|0x0409|Latin1_General_CI_AS|
|Filipino (Filipinas)|0x0464|0x0409|Latin1_General_CI_AS|
|Finlandês (Finlândia)|0x040b|0x040b|Finnish_Swedish_CI_AS|
|Francês (Bélgica)|0x080c|0x040c|French_CI_AS|
|Francês (Canadá)|0x0c0c|0x040c|French_CI_AS|
|Francês (França)|0x040c|0x040c|French_CI_AS|
|Francês (Luxemburgo)|0x140c|0x040c|French_CI_AS|
|Francês (Mônaco)|0x180c|0x040c|French_CI_AS|
|Francês (Suíça)|0x100c|0x040c|French_CI_AS|
|Frisão (Holanda)|0x0462|0x0462|Latin1_General_CI_AI|
|Galego (Espanha)|0x0456|0x0409|Latin1_General_CI_AS|
|Georgiano (Geórgia)|0x10437|0x10437|Georgian_Modern_Sort_CI_AS|
|Georgiano (Geórgia)|0x0437|0x0419|Latin1_General_CI_AS|
|Alemão – classificação do catálogo telefônico (DIN)|0x10407|0x10407|German_PhoneBook_CI_AS|
|Alemão (Áustria)|0x0c07|0x0409|Latin1_General_CI_AS|
|Alemão (Alemanha)|0x0407|0x0409|Latin1_General_CI_AS|
|Alemão (Liechtenstein)|0x1407|0x0409|Latin1_General_CI_AS|
|Alemão (Luxemburgo)|0x1007|0x0409|Latin1_General_CI_AS|
|Alemão (Suíça)|0x0807|0x0409|Latin1_General_CI_AS|
|Grego (Grécia)|0x0408|0x0408|Greek_CI_AS|
|Groenlandês (Groenlândia)|0x046f|0x0406|Danish_Norwegian_CI_AS|
|Gujarati (Índia)|0x0447|0x0439|Indisponível no nível do servidor|
|hauçá (Nigéria, Latino)|0x0468|0x0409|Latin1_General_CI_AS|
|Hebraico (Israel)|0x040d|0x040d|Hebrew_CI_AS|
|Híndi (Índia)|0x0439|0x0439|Indisponível no nível do servidor|
|Húngaro (Hungria)|0x040e|0x040e|Hungarian_CI_AS|
|Classificação Técnica Húngara|0x1040e|0x1040e|Hungarian_Technical_CI_AS|
|Islandês (Islândia)|0x040f|0x040f|Icelandic_CI_AS|
|Igbo (Nigéria)|0x0470|0x0409|Latin1_General_CI_AS|
|Indonésio (Indonésia)|0x0421|0x0409|Latin1_General_CI_AS|
|Inuktitut (Canadá, latino)|0x085d|0x0409|Latin1_General_CI_AS|
|Inuktitut (silábico) Canadá|0x045d|0x045d|Latin1_General_CI_AI|
|Irlandês (Irlanda)|0x083c|0x0409|Latin1_General_CI_AS|
|Italiano (Itália)|0x0410|0x0409|Latin1_General_CI_AS|
|Italiano (Suíça)|0x0810|0x0409|Latin1_General_CI_AS|
|Japonês (Japão XJIS)|0x0411|0x0411|Japanese_CI_AS|
|Japonês (Japão)|0x040411|0x40411|Latin1_General_CI_AI|
|canarim (Índia)|0x044b|0x0439|Indisponível no nível do servidor|
|Cazaque (Cazaquistão)|0x043f|0x043f|Kazakh_90_CI_AS|
|Khmer (Camboja)|0x0453|0x0453|Indisponível no nível do servidor|
|Quiché (Guatemala)|0x0486|0x0c0a|Modern_Spanish_CI_AS|
|Quiniaruanda (Ruanda)|0x0487|0x0409|Latin1_General_CI_AS|
|Konkani (Índia)|0x0457|0x0439|Indisponível no nível do servidor|
|Coreano (classificação de dicionário coreano)|0x0412|0x0412|Korean_Wansung_CI_AS|
|Quirguiz (Quirguistão)|0x0440|0x0419|Cyrillic_General_CI_AS|
|Laosiano (RDP do Laos)|0x0454|0x0454|Indisponível no nível do servidor|
|Letão (Letônia)|0x0426|0x0426|Latvian_CI_AS|
|Lituano (Lituânia)|0x0427|0x0427|Lithuanian_CI_AS|
|Sorábio baixo (Alemanha)|0x082e|0x0409|Latin1_General_CI_AS|
|Luxemburguês (Luxemburgo)|0x046e|0x0409|Latin1_General_CI_AS|
|Macedônio (Macedônia, Antiga República Iugoslava da Macedônia)|0x042f|0x042f|Macedonian_FYROM_90_CI_AS|
|Malaio (Brunei Darussalam)|0x083e|0x0409|Latin1_General_CI_AS|
|Malaio (Malásia)|0x043e|0x0409|Latin1_General_CI_AS|
|Malaiala (Índia)|0x044c|0x0439|Indisponível no nível do servidor|
|Maltês (Malta)|0x043a|0x043a|Latin1_General_CI_AI|
|Maori (Nova Zelândia)|0x0481|0x0481|Latin1_General_CI_AI|
|Mapudungun (Chile)|0x047a|0x047a|Latin1_General_CI_AI|
|Marati (Índia)|0x044e|0x0439|Indisponível no nível do servidor|
|moicano (Canadá)|0x047c|0x047c|Latin1_General_CI_AI|
|Mongol (Mongólia)|0x0450|0x0419|Cyrillic_General_CI_AS|
|Mongol (RPC)|0x0850|0x0419|Cyrillic_General_CI_AS|
|Nepalês (Nepal)|0x0461|0x0461|Indisponível no nível do servidor|
|Norueguês, (Bokmål, Noruega)|0x0414|0x0414|Latin1_General_CI_AI|
|Norueguês (Nynorsk, Noruega)|0x0814|0x0414|Latin1_General_CI_AI|
|occitânico (França)|0x0482|0x040c|French_CI_AS|
|Oriá (Índia)|0x0448|0x0439|Indisponível no nível do servidor|
|Pashto (Afeganistão)|0x0463|0x0463|Indisponível no nível do servidor|
|Persa (Irã)|0x0429|0x0429|Latin1_General_CI_AI|
|Polonês (Polônia)|0x0415|0x0415|Polish_CI_AS|
|Português (Brasil)|0x0416|0x0409|Latin1_General_CI_AS|
|Português (Portugal)|0x0816|0x0409|Latin1_General_CI_AS|
|panjabi (Índia)|0x0446|0x0439|Indisponível no nível do servidor|
|Quíchua (Bolívia)|0x046b|0x0409|Latin1_General_CI_AS|
|Quíchua (Equador)|0x086b|0x0409|Latin1_General_CI_AS|
|Quíchua (Peru)|0x0c6b|0x0409|Latin1_General_CI_AS|
|Romeno (Romênia)|0x0418|0x0418|Romanian_CI_AS|
|Romanche (Suíça)|0x0417|0x0417|Latin1_General_CI_AI|
|Russo (Rússia)|0x0419|0x0419|Cyrillic_General_CI_AS|
|Sami (Inari, Finlândia)|0x243b|0x083b|Latin1_General_CI_AI|
|Sami (Lule, Noruega)|0x103b|0x043b|Latin1_General_CI_AI|
|Sami (Lule, Suécia)|0x143b|0x083b|Latin1_General_CI_AI|
|Sami (Norte, Finlândia)|0x0c3b|0x083b|Latin1_General_CI_AI|
|Sami (Norte, Noruega)|0x043b|0x043b|Latin1_General_CI_AI|
|Sami (Norte, Suécia)|0x083b|0x083b|Latin1_General_CI_AI|
|Sami (Skolt, Finlândia)|0x203b|0x083b|Latin1_General_CI_AI|
|Sami (Sul, Noruega)|0x183b|0x043b|Latin1_General_CI_AI|
|Sami (Sul, Suécia)|0x1c3b|0x083b|Latin1_General_CI_AI|
|Sânscrito (Índia)|0x044f|0x0439|Indisponível no nível do servidor|
|Sérvio (Bósnia e Herzegovina, cirílico)|0x1c1a|0x0c1a|Latin1_General_CI_AI|
|Sérvio (Bósnia e Herzegovina, latino)|0x181a|0x081a|Latin1_General_CI_AI|
|Sérvio (Sérvia, cirílico)|0x0c1a|0x0c1a|Latin1_General_CI_AI|
|Sérvio (Sérvia, latino)|0x081a|0x081a|Latin1_General_CI_AI|
|soto setentrional (África do Sul)|0x046c|0x0409|Latin1_General_CI_AS|
|Setswana/Tswana (África do Sul)|0x0432|0x0409|Latin1_General_CI_AS|
|Cingalês (Sri Lanka)|0x045b|0x0439|Indisponível no nível do servidor|
|Eslovaco (Eslováquia)|0x041b|0x041b|Slovak_CI_AS|
|Esloveno (Eslovênia)|0x0424|0x0424|Slovenian_CI_AS|
|Espanhol (Argentina)|0x2c0a|0x0c0a|Modern_Spanish_CI_AS|
|Espanhol (Bolívia)|0x400a|0x0c0a|Modern_Spanish_CI_AS|
|Espanhol (Chile)|0x340a|0x0c0a|Modern_Spanish_CI_AS|
|Espanhol (Colômbia)|0x240a|0x0c0a|Modern_Spanish_CI_AS|
|Espanhol (Costa Rica)|0x140a|0x0c0a|Modern_Spanish_CI_AS|
|Espanhol (República Dominicana)|0x1c0a|0x0c0a|Modern_Spanish_CI_AS|
|Espanhol (Equador)|0x300a|0x0c0a|Modern_Spanish_CI_AS|
|Espanhol (El Salvador)|0x440a|0x0c0a|Modern_Spanish_CI_AS|
|Espanhol (Guatemala)|0x100a|0x0c0a|Modern_Spanish_CI_AS|
|Espanhol (Honduras)|0x480a|0x0c0a|Modern_Spanish_CI_AS|
|Espanhol (México)|0x080a|0x0c0a|Modern_Spanish_CI_AS|
|Espanhol (Nicarágua)|0x4c0a|0x0c0a|Modern_Spanish_CI_AS|
|Espanhol (Panamá)|0x180a|0x0c0a|Modern_Spanish_CI_AS|
|Espanhol (Paraguai)|0x3c0a|0x0c0a|Modern_Spanish_CI_AS|
|Espanhol (Peru)|0x280a|0x0c0a|Modern_Spanish_CI_AS|
|Espanhol (Porto Rico)|0x500a|0x0c0a|Modern_Spanish_CI_AS|
|Espanhol (Espanha)|0x0c0a|0x0c0a|Modern_Spanish_CI_AS|
|Espanhol (Espanha, classificação tradicional)|0x040a|0x040a|Traditional_Spanish_CI_AS|
|Espanhol (Estados Unidos)|0x540a|0x0409|Latin1_General_CI_AS|
|Espanhol (Uruguai)|0x380a|0x0c0a|Modern_Spanish_CI_AS|
|Espanhol (Venezuela)|0x200a|0x0c0a|Modern_Spanish_CI_AS|
|Suaíle (Quênia)|0x0441|0x0409|Latin1_General_CI_AS|
|Sueco (Finlândia)|0x081d|0x040b|Finnish_Swedish_CI_AS|
|Sueco (Suécia)|0x041d|0x040b|Finnish_Swedish_CI_AS|
|Siríaco (Síria)|0x045a|0x045a|Indisponível no nível do servidor|
|Tadjique (Tadjiquistão)|0x0428|0x0419|Cyrillic_General_CI_AS|
|Tamazirte (Argélia, latino)|0x085f|0x085f|Latin1_General_CI_AI|
|Tâmil (Índia)|0x0449|0x0439|Indisponível no nível do servidor|
|Tatárico (Rússia)|0x0444|0x0444|Cyrillic_General_CI_AS|
|Télugo (Índia)|0x044a|0x0439|Indisponível no nível do servidor|
|Tailandês (Tailândia)|0x041e|0x041e|Thai_CI_AS|
|Tibetano (RPC)|0x0451|0x0451|Indisponível no nível do servidor|
|Turco (Turquia)|0x041f|0x041f|Turkish_CI_AS|
|Turcomeno (Turcomenistão)|0x0442|0x0442|Latin1_General_CI_AI|
|Uighur (RPC)|0x0480|0x0480|Latin1_General_CI_AI|
|Ucraniano (Ucrânia)|0x0422|0x0422|Ukrainian_CI_AS|
|Sorábio Alto (Alemanha)|0x042e|0x042e|Latin1_General_CI_AI|
|Urdu (Paquistão)|0x0420|0x0420|Latin1_General_CI_AI|
|Uzbeque (Uzbequistão, cirílico)|0x0843|0x0419|Cyrillic_General_CI_AS|
|Uzbeque (Uzbequistão, latino)|0x0443|0x0443|Uzbek_Latin_90_CI_AS|
|Vietnamita (Vietnã)|0x042a|0x042a|Vietnamese_CI_AS|
|Galês (Reino Unido)|0x0452|0x0452|Latin1_General_CI_AI|
|uolofe (Senegal)|0x0488|0x040c|French_CI_AS|
|Xhosa/isiXhosa (África do Sul)|0x0434|0x0409|Latin1_General_CI_AS|
|Yakut (Rússia)|0x0485|0x0485|Latin1_General_CI_AI|
|Yi (RPC)|0x0478|0x0409|Latin1_General_CI_AS|
|Ioruba (Nigéria)|0x046a|0x0409|Latin1_General_CI_AS|
|Zulu/isiZulu (África do Sul)|0x0435|0x0409|Latin1_General_CI_AS|

> [!NOTE]
> As ordenações somente Unicode não podem ser selecionadas durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], pois não são compatíveis como ordenações no nível de servidor.    
    
Depois de atribuir uma ordenação ao servidor, você só poderá alterá-la exportando todos os objetos de banco de dados e dados, recriando o banco de dados *mestre* e importando todos os objetos de banco de dados e dados. Em vez de alterar a ordenação padrão de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode especificar a ordenação desejada ao criar um banco de dados ou uma coluna de banco de dados.    

Para consultar a ordenação do servidor para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use a função `SERVERPROPERTY`:

```sql
SELECT CONVERT(varchar, SERVERPROPERTY('collation'));
```

Para consultar o servidor por todas as ordenações disponíveis, use a seguinte função interna `fn_helpcollations()`:

```sql
SELECT * FROM sys.fn_helpcollations();
```
    
#### <a name="Database-level-collations"></a> Ordenações do nível do banco de dados    
Ao criar ou modificar um banco de dados, use a cláusula `COLLATE` da instrução `CREATE DATABASE` ou `ALTER DATABASE` para especificar a ordenação de banco de dados padrão. Se nenhuma ordenação for especificada, o banco de dados receberá a ordenação do servidor.    
    
Não é possível alterar a ordenação de bancos de dados do sistema, a menos que você altere a ordenação para o servidor.
    
A ordenação de banco de dados é usada para todos os metadados no banco de dados, e a ordenação é o padrão para todas as colunas de cadeia de caracteres, objetos temporários, nomes de variáveis e todas as outras cadeias de caracteres usadas no banco de dados. Quando você altera a ordenação de um banco de dados de usuário, pode haver conflitos de ordenação quando consultas no banco de dados acessam tabelas temporárias. Sempre são armazenadas tabelas temporárias no banco de dados do sistema *tempdb* que usa a ordenação para a instância. As consultas que comparam dados de caractere entre o banco de dados de usuário e *tempdb* poderão falhar se as ordenações causarem um conflito ao avaliar os dados de caractere. Resolva esse problema especificando a cláusula `COLLATE` na consulta. Para obter mais informações, confira [COLLATE (Transact-SQL)](~/t-sql/statements/collations.md).    

> [!NOTE]
> Não é possível alterar a ordenação depois que o banco de dados for criado no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Altere a ordenação de um banco de dados de usuário usando uma instrução `ALTER DATABASE` semelhante à seguinte:

```sql
ALTER DATABASE myDB COLLATE Greek_CS_AI;
```

> [!IMPORTANT]
> A alteração da ordenação no nível de banco de dados não afeta as ordenações no nível de coluna ou de expressão.

Recupere a ordenação atual de um banco de dados usando uma instrução semelhante à seguinte:

```sql
SELECT CONVERT (VARCHAR(50), DATABASEPROPERTYEX('database_name','collation'));
```

#### <a name="Column-level-collations"></a> Ordenações em nível de coluna    
Ao criar ou alterar uma tabela, você pode especificar ordenações para cada coluna de cadeia de caracteres usando a cláusula `COLLATE`. Se você não especificar uma ordenação, a coluna será atribuída à ordenação padrão do banco de dados.    

Altere a ordenação de uma coluna usando uma instrução `ALTER TABLE` semelhante à seguinte:

```sql
ALTER TABLE myTable ALTER COLUMN mycol NVARCHAR(10) COLLATE Greek_CS_AI;
```
    
#### <a name="Expression-level-collations"></a> Ordenações no nível da expressão    
As ordenações no nível de expressão são definidas quando uma instrução é executada e afetam o modo como um conjunto de resultados é retornado. Isso permite que os resultados da classificação `ORDER BY` sejam específicos da localidade. Para implementar ordenações no nível da expressão, use uma cláusula `COLLATE` como a seguinte:    
    
```sql    
SELECT name FROM customer ORDER BY name COLLATE Latin1_General_CS_AI;    
```    
    
###  <a name="Locale_Defn"></a> Localidade    
Uma localidade é um conjunto de informações associadas a uma localização ou uma cultura. As informações podem incluir o nome e o identificador do idioma falado, o script usado para escrever o idioma e as convenções culturais. As ordenações podem ser associadas a uma ou mais localidades. Para obter mais informações, consulte o artigo sobre [IDs de localidade atribuídas pela Microsoft](https://msdn.microsoft.com/goglobal/bb964664.aspx).    
    
###  <a name="Code_Page_Defn"></a> Página de código    
Uma página de código é um conjunto de caracteres ordenado de um determinado script no qual um índice numérico ou valor de ponto de código é associado a cada caractere. Uma página de código do Windows geralmente é referenciada como um *conjunto de* *caracteres*. As páginas de código são usadas para oferecer suporte aos conjuntos de caracteres e layouts de teclado usados por diferentes localidades de sistema do Windows.     
 
###  <a name="Sort_Order_Defn"></a> Ordem de classificação    
A ordem de classificação especifica como os valores de dados são classificados. A ordem afeta os resultados da comparação de dados. Os dados são classificados com o uso de ordenações e podem ser otimizados com o uso de índices.    
    
##  <a name="Unicode_Defn"></a> Suporte a Unicode    
O Unicode é um padrão para mapear pontos de código para caracteres. Como ele foi projetado para abranger todos os caracteres de todos os idiomas do mundo, você não precisa ter páginas de código diferentes para manipular diferentes conjuntos de caracteres.

### <a name="unicode-basics"></a>Noções básicas de Unicode
O armazenamento de dados em vários idiomas em um banco de dados é difícil de administrar quando você usa apenas dados de caracteres e páginas de código. Também é difícil encontrar uma página de código para o banco de dados que possa armazenar todos os caracteres necessários específicos a um idioma. Além disso, é difícil garantir a tradução correta de caracteres especiais quando eles são lidos ou atualizados por uma variedade de clientes que executam várias páginas de código. Bancos de dados que oferecem suporte a clientes internacionais sempre deveriam usar tipos de dados Unicode em vez de tipos de dados não Unicode.

Por exemplo, considere um banco de dados de clientes na América do Norte que deve lidar com três idiomas principais:

-  Nomes e endereços em espanhol para o México
-  Nomes e endereços em francês para Quebec
-  Nomes e endereços em inglês para o resto do Canadá e dos Estados Unidos

Ao usar apenas colunas de caracteres e páginas de código, você deve tomar cuidado para garantir que o banco de dados seja instalado com uma página de código que manipule os caracteres dos três idiomas. Você também precisa tomar cuidado para garantir a tradução correta de caracteres de um dos idiomas, quando os caracteres forem lidos por clientes que executam uma página de código de outro idioma.
   
> [!NOTE]
> As páginas de código usadas por um cliente são determinadas pelas configurações do SO (sistema operacional). Para definir páginas de código de cliente no sistema operacional Windows, use **Configurações Regionais** no Painel de Controle.    

É difícil selecionar uma página de código para tipos de dados de caractere que dará suporte a todos os caracteres necessários para um público-alvo mundial. A maneira mais fácil de gerenciar dados de caractere em bancos de dados internacionais é sempre usar um tipo de dados com suporte a Unicode. 

### <a name="unicode-data-types"></a>Tipos de dados Unicode
Se você armazenar dados de caractere que refletem várias linguagens no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e posterior), use tipos de dados Unicode (**nchar**, **nvarchar** e **ntext**) em vez de tipos de dados não Unicode (**char**, **varchar** e **text**). 

> [!NOTE]
> No caso dos tipos de dados Unicode, o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] poderá representar até 65.535 caracteres usando o UCS-2 ou o intervalo completo de Unicode (1.114.111 caracteres) se caracteres suplementares forem usados. Para obter mais informações sobre como habilitar caracteres suplementares, confira [Caracteres suplementares](#Supplementary_Characters).

Como alternativa, no [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] em diante, se uma ordenação habilitada para UTF-8 (\_UTF8) for usada, os tipos de dados que eram não Unicode (**char** e **varchar**) se tornarão tipos de dados Unicode usando codificação UTF-8. [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] não altera o comportamento dos tipos de dados Unicode anteriormente existentes (**nchar**, **nvarchar** e **ntext**), que continuam usando a codificação UCS-2 ou UTF-16. Para obter mais informações, confira [Diferenças de armazenamento entre UTF-8 e UTF-16](#storage_differences).

### <a name="unicode-considerations"></a>Considerações sobre Unicode
Limitações consideráveis estão associadas a tipos de dados não Unicode. Isso ocorre porque um computador não Unicode fica limitado a usar uma única página de código. Você pode ter um ganho de desempenho com o uso de Unicode, porque ele exige menos conversões de página de código. As ordenações Unicode precisam ser selecionadas individualmente no nível de banco de dados, coluna ou expressão, porque não há suporte para elas no nível de servidor.    

Quando você move dados de um servidor para um cliente, a ordenação do servidor pode não ser reconhecida por drivers de cliente mais antigos. Isso pode ocorrer quando você move dados de um servidor Unicode para um cliente não Unicode. A melhor opção pode ser atualizar o sistema operacional do cliente para que as ordenações de sistema subjacentes sejam atualizadas. Se houver um software de cliente de banco de dados instalado no cliente, você deverá considerar a possibilidade de aplicar uma atualização de serviço a esse software.    
    
> [!TIP]
> Você também pode tentar usar uma ordenação diferente para os dados no servidor. Escolha uma ordenação que mapeia para uma página de código no cliente.    
>
> Para usar as ordenações UTF-16 disponíveis no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior) visando melhorar a pesquisa e a classificação de alguns caracteres Unicode (somente ordenações do Windows), selecione uma das ordenações de caracteres suplementares (\_SC) ou uma das ordenações da versão 140.    
 
Para usar as ordenações UTF-8 disponíveis no [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] e melhorar a pesquisa e a classificação de alguns caracteres Unicode (somente ordenações do Windows), você precisará selecionar ordenações habilitadas para codificação UTF-8 (\_UTF8).
 
-   O sinalizador de UTF8 pode ser aplicado a:    
    -   Ordenações linguísticas que já têm suporte para \_SC (caracteres suplementares) ou com o reconhecimento de \_VSS (diferenciação de seletor de variação)
    -   Ordenação binária BIN2<sup>1</sup>
    
-   O sinalizador de UTF-8 não pode ser aplicado a:    
    -   Ordenações linguísticas que não têm suporte para \_SC (caracteres suplementares) ou com o reconhecimento de \_VSS (diferenciação de seletor de variação)
    -   As ordenações primárias BIN ou BIN2<sup>2</sup>
    -   As ordenações do SQL\_*  
    
<sup>1</sup> No [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.3 em diante. O [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 3.0 substituiu a ordenação **UTF8_BIN2** pela **Latin1_General_100_BIN2_UTF8**.        
<sup>2</sup> Até com o [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.3.    
    
Para avaliar os problemas relacionados ao uso de tipos de dados Unicode ou não Unicode, teste seu cenário para medir as diferenças de desempenho em seu ambiente. Uma boa prática é padronizar a ordenação usada nos sistemas de sua organização e implantar servidores e clientes Unicode sempre que possível.    
    
Na maioria das situações, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interage com outros servidores ou clientes, e a sua organização poderá usar vários padrões de acesso a dados entre aplicativos e instâncias de servidor. Clientes[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são de um destes dois tipos principais:    
    
-   **Clientes Unicode** que usam o OLE DB e o ODBC versão 3.7 ou posterior.    
-   **Clientes não Unicode** que usam a DB-Library e o ODBC versão 3.6 ou anterior.    
    
A seguinte tabela fornece informações sobre como usar dados multilíngues com várias combinações de servidores Unicode e não Unicode:    
    
|Servidor|Cliente|Benefícios ou limitações|    
|------------|------------|-----------------------------|    
|Unicode|Unicode|Como os dados Unicode são usados em todo o sistema, este cenário fornece o melhor desempenho e proteção contra danos de dados recuperados. É isso o que acontece com a ADO (ActiveX Data Objects), o OLE DB e o ODBC versão 3.7 ou posterior.|    
|Unicode|Não Unicode|Neste cenário, principalmente em conexões entre um servidor que executa um sistema operacional mais recente e um cliente que executa uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou em um sistema operacional mais antigo, pode haver limitações ou erros ao mover os dados para um computador cliente. Os dados Unicode no servidor tentam mapear para uma página de código correspondente no cliente não Unicode para converter os dados.|    
|Não Unicode|Unicode|Essa não é uma configuração ideal para o uso de dados multilíngues. Não é possível gravar dados Unicode no servidor não Unicode. É provável que ocorram problemas quando os dados forem enviados para servidores que estejam fora da página de código do servidor.|    
|Não Unicode|Não Unicode|Este é um cenário muito limitado para dados multilíngues. Você pode usar uma única página de código.|    
    
##  <a name="Supplementary_Characters"></a> Caracteres suplementares    
O Unicode Consortium aloca para cada caractere um ponto de código exclusivo, que é um valor no intervalo 000000–10FFFF. Os caracteres usados com mais frequência têm valores de ponto de código no intervalo 000000–00FFFF (65.535 caracteres) que se ajustam a uma palavra de 8 ou 16 bits na memória e no disco. Geralmente, esse intervalo é designado como BMP (Plano Multilíngue Básico). 

No entanto, o Consortium Unicode estabeleceu 16 "planos" adicionais de caracteres, cada um com o mesmo tamanho do BMP. Essa definição permite ao Unicode o potencial para representar 1.114.112 caracteres (ou seja, 2<sup>16</sup> * 17 caracteres) dentro do intervalo do ponto de código 000000–10FFFF. Os caracteres com valores de ponto de código superiores a 00FFFF exigem duas a quatro palavras consecutivas de 8 bits (UTF-8) ou duas palavras consecutivas de 16 bits (UTF-16). Esses caracteres localizados além do BMP são chamados de *caracteres suplementares*, e as palavras adicionais consecutivas de 8 ou 16 bits são chamadas de *pares alternativos*. Para obter mais informações sobre caracteres suplementares, substitutos e pares alternativos, veja [o Padrão Unicode](http://www.unicode.org/standard/standard.html).    

O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece tipos de dados, como **nchar** e **nvarchar**, para armazenar dados Unicode no intervalo do BMP (000000–00FFFF), que o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] codifica usando UCS-2. 

O [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] introduziu uma nova família de ordenações de caracteres suplementares (\_SC) que podem ser usadas com os tipos de dados **nchar**, **nvarchar** e **sql_variant** para representar o intervalo completo de caracteres Unicode (000000–10FFFF). Por exemplo:  **Latin1_General_100_CI_AS_SC** ou, se você estiver usando uma ordenação de japonês, **Japanese_Bushu_Kakusu_100_CI_AS_SC**. 
 
[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] estende o suporte a caracteres suplementares aos tipos de dados **char** e **varchar** com as novas ordenações habilitadas para UTF-8 ([\_UTF8](#utf8)). Esses tipos de dados também podem representar o intervalo completo de caracteres Unicode.   

> [!NOTE]
> No [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] em diante, todas as novas ordenações da versão \_140 automaticamente dão suporte a caracteres suplementares.

Se você usar caracteres suplementares:    
    
-   Caracteres suplementares podem ser usados apenas em operações de comparação e ordenação em versões de ordenação 90 ou superior.    
-   Todas as ordenações de versão 100 dão suporte à classificação linguística com caracteres suplementares.    
-   Os caracteres suplementares não são compatíveis para uso em metadados, como em nomes de objetos de banco de dados.    
-   O sinalizador de SC pode ser aplicado a:    
    -   Ordenações da versão 90    
    -   Ordenações da versão 100    
    
-   O sinalizador de SC não pode ser aplicado a:    
    -   Ordenações do Windows sem versão na versão 80    
    -   As ordenações primárias BIN ou BIN2    
    -   As ordenações do SQL\*    
    -   Ordenações da versão 140 (elas não precisam do sinalizador de SC, pois já dão suporte a caracteres suplementares)    
    
A seguinte tabela compara o comportamento de alguns operadores e funções de cadeia de caracteres quando eles usam caracteres suplementares com e sem uma ordenação SCA (reconhecimento de caracteres suplementares):    
    
|Operador ou função de cadeia de caracteres|Com uma ordenação de SCA|Sem uma ordenação de SCA|    
|---------------------------------|--------------------------|-----------------------------|    
|[CHARINDEX](../../t-sql/functions/charindex-transact-sql.md)<br /><br /> [LEN](../../t-sql/functions/len-transact-sql.md)<br /><br /> [PATINDEX](../../t-sql/functions/patindex-transact-sql.md)|O par alternativo UTF-16 é contado como um único ponto de código.|O par alternativo UTF-16 é contado como dois pontos de código.|    
|[LEFT](../../t-sql/functions/left-transact-sql.md)<br /><br /> [REPLACE](../../t-sql/functions/replace-transact-sql.md)<br /><br /> [REVERSE](../../t-sql/functions/reverse-transact-sql.md)<br /><br /> [RIGHT](../../t-sql/functions/right-transact-sql.md)<br /><br /> [SUBSTRING](../../t-sql/functions/substring-transact-sql.md)<br /><br /> [STUFF](../../t-sql/functions/stuff-transact-sql.md)|Essas funções tratam cada par alternativo como um único ponto de código e funcionam conforme esperado.|Essas funções podem dividir qualquer par alternativo e levar a resultados inesperados.|    
|[NCHAR](../../t-sql/functions/nchar-transact-sql.md)|Retorna o caractere que corresponde ao valor do ponto de código Unicode especificado no intervalo 0–0x10FFFF. Se o valor especificado estiver no intervalo 0–0xFFFF, um caractere será retornado. Para valores mais altos, é retornado o substituto correspondente.|Um valor mais alto que 0xFFFF retorna NULL, em vez do substituto correspondente.|    
|[UNICODE](../../t-sql/functions/unicode-transact-sql.md)|Retorna um ponto de código UTF-16 no intervalo 0–0x10FFFF.|Retorna um ponto de código UCS-2 no intervalo 0–0xFFFF.|    
|[Corresponder a um caractere curinga](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)<br /><br /> [Curinga – caracter(es) para não corresponder](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)|Há suporte para caracteres suplementares para todas as operações de curingas.|Não há suporte para caracteres suplementares nessas operações de curingas. Há suporte para outros operadores curinga.|    
    
## <a name="GB18030"></a> Suporte a GB18030    
GB18030 é um padrão separado usado na República Popular da China para codificar caracteres chineses. Em GB18030, caracteres podem ter 1, 2 ou 4 bytes em comprimento. O[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte a caracteres GB18030 codificados, reconhecendo-os quando eles entram no servidor, provenientes de um aplicativo cliente, convertendo-os e armazenando-os nativamente como caracteres Unicode. Depois de serem armazenados no servidor, eles são tratados como caracteres Unicode em todas as operações seguintes. 

Você pode usar qualquer ordenação em chinês, preferivelmente a mais recente versão 100. Todas as ordenações de nível \_100 dão suporte à classificação linguística com caracteres GB18030. Se os dados incluírem caracteres suplementares (pares alternativos), você poderá usar as ordenações de SC disponíveis no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para melhorar a pesquisa e a classificação.    

> [!NOTE]
> Verifique se as ferramentas de cliente, como [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], usam a fonte Dengxian para exibir corretamente cadeias de caracteres que contêm caracteres codificados em GB18030.
    
## <a name="Complex_script"></a> Suporte a script complexo    
O[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte à inserção, armazenamento, alteração e exibição de scripts complexos. Scripts complexos incluem os seguintes tipos:    
    
-   Scripts que incluem uma combinação de texto da direita para a esquerda e da esquerda para a direita, como uma combinação de texto em árabe e inglês.    
-   Scripts cujos caracteres alteram de forma de acordo com sua posição ou quando combinados com outros caracteres, como caracteres árabes, índicos e tailandeses.    
-   Idiomas, como o tailandês, que exigem dicionários internos para reconhecer palavras, porque não há nenhuma quebra entre eles.    
    
Aplicativos de banco de dados que interagem com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devem usar controles que oferecem suporte a scripts complexos. Os controles de formulário padrão do Windows que são criados em código gerenciado são habilitados para script complexo.    

## <a name="Japanese_Collations"></a> Ordenações de japonês adicionadas ao [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]
 
No [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] em diante, há suporte para duas novas famílias de ordenação de japonês, com as permutações de várias opções (\_CS, \_AS, \_KS, \_WS e \_VSS). 

Para listar essas ordenações, você pode consultar o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]:      

```sql 
SELECT Name, Description FROM fn_helpcollations()  
WHERE Name LIKE 'Japanese_Bushu_Kakusu_140%' OR Name LIKE 'Japanese_XJIS_140%'
``` 

Todas as novas ordenações têm suporte interno para caracteres suplementares, de modo que nenhuma das novas ordenações da versão **\_140** têm (ou precisa de) sinalizador de SC.

Essas ordenações são compatíveis com índices, tabelas com otimização de memória, índices columnstore e módulos compilados nativamente no [!INCLUDE[ssde_md](../../includes/ssde_md.md)].

<a name="ctp23"></a>

## <a name="utf8"></a> Suporte para UTF-8
O [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] apresenta suporte completo para a codificação de caracteres UTF-8 amplamente utilizada como codificação de importação ou exportação e como ordenação em nível de coluna ou de banco de dados para dados de cadeia de caracteres. O UTF-8 é permitido nos tipos de dados **char** e **varchar** e é habilitado quando você cria ou altera a ordenação de um objeto para um ordenação que tem um sufixo *UTF8*. Um exemplo é alterar **LATIN1_GENERAL_100_CI_AS_SC** para **LATIN1_GENERAL_100_CI_AS_SC_UTF8**. 

O UTF-8 só está disponível para ordenações do Windows que dão suporte a caracteres suplementares, conforme introduzido no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Os tipos de dados **nchar** e **nvarchar** permitem apenas a codificação UCS-2 ou UTF-16 e permanecem inalterados.

### <a name="storage_differences"></a> Diferenças de armazenamento entre UTF-8 e UTF-16
O Unicode Consortium aloca para cada caractere um ponto de código exclusivo, que é um valor no intervalo 000000–10FFFF. Com o [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)], as codificações em UTF-8 e UTF-16 estão disponíveis para representar o intervalo completo:    
-  Com a codificação UTF-8, os caracteres no intervalo do ASCII (000000–00007F) exigem 1 byte, os pontos de código 000080–0007FF exigem 2 bytes, os pontos de código 000800–00FFFF exigem 3 bytes e os pontos de código 0010000–0010FFFF exigem 4 bytes. 
-  Com a codificação UTF-16, os pontos de código 000000–00FFFF exigem 2 bytes e os pontos de código 0010000–0010FFFF exigem 4 bytes. 

A seguinte tabela lista os bytes de armazenamento de codificação para cada intervalo de caracteres e tipo de codificação:

|Intervalo de códigos (hexadecimal)|Intervalo de códigos (decimal)|Bytes de armazenamento<sup>1</sup> com UTF-8|Bytes de armazenamento<sup>1</sup> com UTF-16|    
|---------------------------------|---------------------------------|--------------------------|-----------------------------|   
|000000–00007F|0–127|1|2|
|000080–00009F<br />0000A0–0003FF<br />000400–0007FF|128–159<br />160–1.023<br />1\.024–2.047|2|2|
|000800–003FFF<br />004000–00FFFF|2\.048–16.383<br />16.384–65.535|3|2|
|010000–03FFFF<sup>2</sup><br /><br />040000–10FFFF<sup>2</sup>|65.536–262.143<sup>2</sup><br /><br />262.144–1.114.111<sup>2</sup>|4|4|

<sup>1</sup> *Bytes de armazenamento* se referem ao tamanho do byte codificado e não ao tamanho do armazenamento em disco do tipo de dados. Para saber mais sobre tamanhos de armazenamento em disco, confira os tipos de dados [nchar e nvarchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md) e [char e varchar](../../t-sql/data-types/char-and-varchar-transact-sql.md).

<sup>2</sup> O intervalo do ponto de código para [caracteres suplementares](#Supplementary_Characters).

> [!TIP]   
> É comum pensar, em [CHAR(*n*) e VARCHAR(*n*)](../../t-sql/data-types/char-and-varchar-transact-sql.md) ou em [NCHAR(*n*) e NVARCHAR(*n*)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md), que *n*define o número de caracteres. Isso ocorre porque, no exemplo de uma coluna CHAR(10), 10 caracteres ASCII no intervalo 0–127 podem ser armazenados usando uma ordenação como **Latin1_General_100_CI_AI**, porque cada caractere desse intervalo usa apenas 1 byte.
>    
> No entanto, em [CHAR(*n*) e VARCHAR(*n*)](../../t-sql/data-types/char-and-varchar-transact-sql.md), *n* define o tamanho da cadeia de caracteres em *bytes* (0–8.000), e em [NCHAR(*n*) e NVARCHAR(*n*)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md), *n* define o tamanho da cadeia de caracteres em *pares de bytes* (0–4.000). *n* nunca define números de caracteres que podem ser armazenados.

Como você acabou de ver, a escolha do tipo de dados e da codificação Unicode apropriados pode proporcionar uma economia significativa de armazenamento ou aumentar o volume de armazenamento atual, dependendo do conjunto de caracteres em uso. Por exemplo, quando você usa uma ordenação de latim que é habilitada para UTF-8, como **Latin1_General_100_CI_AI_SC_UTF8**, uma coluna `CHAR(10)` armazena 10 bytes e pode conter 10 caracteres ASCII no intervalo 0–127. No entanto, ela pode conter apenas cinco caracteres no intervalo de 128–2.047 e apenas três caracteres no intervalo de 2.048–65.535. Por comparação, como uma coluna `NCHAR(10)` armazena 10 pares de bytes (20 bytes), ela pode armazenar 10 caracteres no intervalo de 0–65.535.  

Antes de optar por usar a codificação UTF-8 ou UTF-16 para um banco de dados ou uma coluna, considere a distribuição dos dados de cadeia de caracteres que serão armazenados:
-  Se a maioria estiver no intervalo 0–127 do ASCII (como o inglês), cada caractere exigirá 1 byte com UTF-8 e 2 bytes com UTF-16. O uso de UTF-8 proporciona vantagens de armazenamento. A alteração de um tipo de dados de coluna existente com caracteres ASCII no intervalo 0–127 de `NCHAR(10)` para `CHAR(10)` e o uso de uma ordenação habilitada para UTF-8 representam 50% de redução nos requisitos de armazenamento. Essa redução ocorre porque `NCHAR(10)` exige 20 bytes para armazenamento, em comparação com `CHAR(10)`, que exige 10 bytes para a mesma representação de cadeia de caracteres Unicode.    
-  Acima do intervalo do ASCII, quase todos os scripts com base latina, além do grego, cirílico, copta, armênio, hebraico, árabe, siríaco, tāna e n'ko, exigem 2 bytes por caractere em UTF-8 e UTF-16. Nesses casos, não há diferenças significativas de armazenamento para tipos de dados comparáveis (por exemplo, entre o uso de **char** ou **nchar**).
-  Se a maioria for de scripts do Leste Asiático (como coreano, chinês e japonês), cada caractere exigirá 3 bytes com UTF-8 e 2 bytes com UTF-16. O uso de UTF-16 proporciona vantagens de armazenamento. 
-  Os caracteres no intervalo de 010000–10FFFF exigem 4 bytes tanto em UTF-8 quanto em UTF-16. Nesses casos, não há diferenças de armazenamento para tipos de dados comparáveis (por exemplo, entre o uso de **char** ou **nchar**).

Para ver outras considerações, confira o artigo [Gravar instruções Transact-SQL internacionais](../../relational-databases/collations/write-international-transact-sql-statements.md).

### <a name="converting"></a> Como converter em UTF-8
Como em [CHAR (*n*) e VARCHAR (*n*)](../../t-sql/data-types/char-and-varchar-transact-sql.md) ou em [NCHAR (*n*) e NVARCHAR (*n*)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md), o *n* define o tamanho de armazenamento em bytes, não o número de caracteres que podem ser armazenados, é importante determinar o tamanho do tipo de dados para o qual você deve converter para evitar o truncamento de dados. 

Por exemplo, considere uma coluna definida como **NVARCHAR (100)** que armazena 180 bytes de caracteres japoneses. Neste exemplo, os dados da coluna atualmente são codificados usando UCS-2 ou UTF-16, que usa 2 bytes por caractere. A conversão do tipo de coluna para **VARCHAR (200)** não é suficiente para evitar o truncamento de dados, pois o novo tipo de dados só pode armazenar 200 bytes, mas os caracteres japoneses exigem 3 bytes quando codificados em UTF-8. Portanto, a coluna deve ser definida como **VARCHAR (270)** para evitar a perda de dados por truncamento de dados.

Portanto, é necessário saber com antecedência qual é o tamanho do byte projetado para a definição da coluna antes de converter os dados existentes em UTF-8 e ajustar o tamanho do novo tipo de dados de acordo. Confira o script [!INCLUDE[tsql](../../includes/tsql-md.md)] ou o SQL Notebook no [GitHub de exemplos de dados](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/unicode), que usa a função [DATALENGTH](../../t-sql/functions/datalength-transact-sql.md) e a instrução [COLLATE](../../t-sql/statements/collations.md) para determinar os requisitos de comprimento de dados corretos para operações de conversão UTF-8 em um banco de dados existente.

Para alterar a ordenação de colunas e o tipo de dados em uma tabela existente, use um dos métodos descritos em [Definir ou alterar a ordenação de colunas](../../relational-databases/collations/set-or-change-the-column-collation.md).

Para alterar a ordenação do banco de dados, permitindo que novos objetos herdem a ordenação de banco de dados por padrão ou alterem a ordenação do servidor, permitindo que novos bancos de dados herdem a ordenação do sistema por padrão, confira a seção [Tarefas relacionadas](#Related_Tasks) deste artigo. 

##  <a name="Related_Tasks"></a> Related tasks    
    
|Tarefa|Tópico|    
|----------|-----------|    
|Descreve como definir ou alterar a ordenação da instância de SQL Server. Observe que alterar a ordenação do servidor não altera a ordenação dos bancos de dados existentes.|[Definir ou alterar a ordenação do servidor](../../relational-databases/collations/set-or-change-the-server-collation.md)|    
|Descreve como definir ou alterar a ordenação de um banco de dados de usuário. Observe que a alteração de uma ordenação do banco de dados não altera a ordenação de colunas de tabela existentes.|[Definir ou alterar a ordenação de banco de dados](../../relational-databases/collations/set-or-change-the-database-collation.md)|    
|Descreve como definir ou alterar a ordenação de uma coluna no banco de dados|[Definir ou alterar a ordenação de coluna](../../relational-databases/collations/set-or-change-the-column-collation.md)|    
|Descreve como retornar informações de ordenação no nível de servidor, de banco de dados ou de coluna|[Exibir informações de ordenação](../../relational-databases/collations/view-collation-information.md)|    
|Descreve como escrever instruções Transact-SQL que tenham mais portabilidade de um idioma para outro ou que deem suporte a vários idiomas com mais facilidade|[Gravar instruções Transact-SQL internacionais](../../relational-databases/collations/write-international-transact-sql-statements.md)|    
|Descreve como alterar o idioma de mensagens de erro e preferências de como a data, a hora e os dados de moeda são usados e exibidos|[Definir um idioma de sessão](../../relational-databases/collations/set-a-session-language.md)|    
    
##  <a name="Related_Content"></a> Related content    
Para obter mais informações, confira o seguinte conteúdo relacionado:
* [Práticas recomendadas para alteração em ordenações do SQL Server](https://go.microsoft.com/fwlink/?LinkId=113891)  
* [Usar o formato de caractere Unicode para importar ou exportar dados (SQL Server)](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)
* [Gravar instruções Transact-SQL internacionais](../../relational-databases/collations/write-international-transact-sql-statements.md)  
* [Melhores práticas de migração para Unicode do SQL Server](https://go.microsoft.com/fwlink/?LinkId=113890) (deixou de receber manutenção)   
* [Unicode Consortium](https://go.microsoft.com/fwlink/?LinkId=48619)  
* [Padrão Unicode](http://www.unicode.org/standard/standard.html)  
* [Suporte ao UTF-8 no OLE DB Driver for SQL Server](../../connect/oledb/features/utf-8-support-in-oledb-driver-for-sql-server.md)  
* [Nome de ordenação do SQL Server (Transact-SQL)](../../t-sql/statements/sql-server-collation-name-transact-sql.md)  
* [Nome de ordenação do Windows (Transact-SQL)](../../t-sql/statements/windows-collation-name-transact-sql.md)  
* [Apresentação do suporte a UTF-8 para SQL Server](https://techcommunity.microsoft.com/t5/SQL-Server/Introducing-UTF-8-support-for-SQL-Server/ba-p/734928)       
    
## <a name="see-also"></a>Confira também    
[Ordenações de banco de dados independentes](../../relational-databases/databases/contained-database-collations.md)     
[Escolher um idioma ao criar um índice de texto completo](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md)     
[sys.fn_helpcollations (Transact-SQL)](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)       
[Conjuntos de caracteres multibyte e de byte único](https://docs.microsoft.com/cpp/c-runtime-library/single-byte-and-multibyte-character-sets)      
 
