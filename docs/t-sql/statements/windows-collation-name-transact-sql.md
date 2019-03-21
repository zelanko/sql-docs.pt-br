---
title: Nome de ordenação do Windows (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Windows collations [SQL Server]
- names [SQL Server], collations
- collations [SQL Server], Windows collations
- Collation Designator
ms.assetid: acceef84-2c68-46e2-a021-be019b7ab14e
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1816363425276ec532e5cc04433630e8e6b9bcac
ms.sourcegitcommit: 03870f0577abde3113e0e9916cd82590f78a377c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/18/2019
ms.locfileid: "57974345"
---
# <a name="windows-collation-name-transact-sql"></a>Nome de ordenação do Windows (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Especifica o nome de ordenação do Windows na cláusula COLLATE em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O nome de ordenação do Windows é composto pelo designador de ordenação e pelos estilos de comparação.

![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>Sintaxe

```

<Windows_collation_name> :: =
CollationDesignator_<ComparisonStyle>

<ComparisonStyle> :: =
{ CaseSensitivity_AccentSensitivity [ _KanatypeSensitive ] [ _WidthSensitive ] [ _VariationSelectorSensitive ] 
}
| { _UTF8 }
| { _BIN | _BIN2 }
```

## <a name="arguments"></a>Argumentos

*CollationDesignator* Especifica as regras de ordenação básicas usadas pela ordenação do Windows. As regras de ordenação básicas abrangem o seguinte:

- As regras de classificação e comparação aplicadas quando a classificação do dicionário é especificada. As regras de classificação são baseadas no alfabeto ou no idioma.
- A página de código usada para armazenar dados **varchar**.

Alguns exemplos são:

- Latin1\_General ou francês: ambos usam a página de código 1252.
- Turco: usa página de código 1254.

*CaseSensitivity*  
**CI** especifica que não diferencia maiúsculas de minúsculas, **CS** especifica que diferencia maiúsculas de minúsculas.

*AccentSensitivity*  
**AI** especifica que não diferencia acentos, **AS** especifica que diferencia acento.

*KanatypeSensitive*  
**Omitido** especifica que não diferencia caracteres kana, **KS** especifica que faz distinção de caracteres kana.

*WidthSensitivity*  
**Omitido** especifica que não diferencia largura, **WS** especifica que distingue largura.

*VariationSelectorSensitivity*  
**Aplica-se ao**: A partir do [!INCLUDE[ssSQL15](../../includes/sssqlv14-md.md)] 

**Omitted** especifica que não diferencia seletor de variação, **VSS** especifica que diferencia seletor de variação.

**UTF8**  
**Aplica-se ao**: A partir do [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]   

Especifica a codificação UTF-8 a ser usada para tipos de dados qualificados. Para obter mais informações, consulte [Suporte a ordenações e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md).

**BIN**  
Especifica a ordem de classificação binária compatível com versões anteriores que será usada.

**BIN2**  
Especifica a ordem de classificação binária que usa semântica de comparação de ponto de código.

## <a name="remarks"></a>Remarks
De acordo com a versão da ordenação, alguns pontos de código podem não ter pesos de classificação e/ou mapeamentos de maiúsculas/minúsculas definidos. Por exemplo, compare a saída da função `LOWER` quando ela recebe o mesmo caractere, mas em diferentes versões da mesma ordenação:

```sql
SELECT NCHAR(504) COLLATE Latin1_General_CI_AS AS [Uppercase],
       NCHAR(505) COLLATE Latin1_General_CI_AS AS [Lowercase];
-- Ǹ    ǹ


SELECT LOWER(NCHAR(504) COLLATE Latin1_General_CI_AS) AS [Version80Collation],
       LOWER(NCHAR(504) COLLATE Latin1_General_100_CI_AS) AS [Version100Collation];
-- Ǹ    ǹ
```

A primeira instrução mostra as formas maiúsculas e minúsculas desse caractere na ordenação mais antiga (a ordenação não afeta a disponibilidade dos caracteres ao trabalhar usando dados Unicode). No entanto, a segunda instrução mostra que um caractere maiúsculo é retornado quando a ordenação é Latin1\_General\_CI\_AS, porque esse ponto de código não tem um mapeamento de minúsculas definido na ordenação em questão.

Ao trabalhar com alguns idiomas, pode ser crítico evitar ordenações mais antigas. Por exemplo, isso se aplica ao télugu.

Em alguns casos, as ordenações do Windows e ordenações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem gerar diferentes planos de consulta para a mesma consulta.

## <a name="examples"></a>Exemplos

A seguir estão alguns exemplos de nomes de ordenação do Windows:

- **Latin1\_General\_100\_CI\_AS**

  A ordenação usa as regras de classificação do dicionário Latin1 Geral e é mapeada para a página de código 1252. É uma versão da ordenação \_100, não diferencia maiúsculas de minúsculas (CI) e diferencia acento (AS).

- **Estonian\_CS\_AS**

  A ordenação usa as regras de classificação do dicionário estoniano e mapeia para a página de código 1257. É uma versão de ordenação \_80 (sem indicação do número de versão no nome), diferencia maiúsculas de minúsculas (CS) e diferencia acento (AS).

- **Japanese\_Bushu\_Kakusu\_140\_BIN2**

  A ordenação usa regras de classificação de ponto de código binário e mapeia para a página de código 932. É uma versão de ordenação \_140 é as regras de classificação do dicionário Japanese Bushu Kakusu são ignoradas.

## <a name="windows-collations"></a>Ordenações do Windows

Para listar as ordenações do Windows suportadas pela instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], execute a seguinte consulta.

```sql
SELECT * FROM sys.fn_helpcollations() WHERE [name] NOT LIKE N'SQL%';
```

A tabela a seguir lista todas as ordenações do Windows com suporte no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].

|Localidade do Windows|Ordenação versão 100|Ordenação versão 90|
|--------------------|---------------------------|--------------------------|
|Alsaciano (França)|Latin1_General_100_|Não disponível|
|Amárico (Etiópia)|Latin1_General_100_|Não disponível|
|Armênio (Armênia)|Cyrillic_General_100_|Não disponível|
|Assamês (Índia)|Assamese_100_ <sup>1</sup>|Não disponível|
|Bashkir (Rússia)|Bashkir_100_|Não disponível|
|Basco (Basco)|Latin1_General_100_|Não disponível|
|Bengali (Bangladesh)|Bengali_100_<sup>1</sup>|Não disponível|
|Bengali (India)|Bengali_100_<sup>1</sup>|Não disponível|
|Bósnio (Bósnia e Herzegovina, Cirílico)|Bosnian_Cyrillic_100_|Não disponível|
|Bósnio (Bósnia e Herzegovina, Latino)|Bosnian_Latin_100_|Não disponível|
|Bretão (França)|Breton_100_|Não disponível|
|Chinese (Macao SAR)|Chinese_Traditional_Pinyin_100_|Não disponível|
|Chinese (Macao SAR)|Chinese_Traditional_Stroke_Order_100_|Não disponível|
|Chinês (Singapura)|Chinese_Simplified_Stroke_Order_100_|Não disponível|
|Corso (França)|Corsican_100_|Não disponível|
|Croata (Bósnia e Herzegovina, Latino)|Croatian_100_|Não disponível|
|Dari (Afeganistão)|Dari_100_|Não disponível|
|Inglês (Índia)|Latin1_General_100_|Não disponível|
|Inglês (Malásia)|Latin1_General_100_|Não disponível|
|Inglês (Singapura)|Latin1_General_100_|Não disponível|
|Filipino (Filipinas)|Latin1_General_100_|Não disponível|
|Frisão (Países Baixos)|Frisian_100_|Não disponível|
|Georgiano (Geórgia)|Cyrillic_General_100_|Não disponível|
|Groenlandês (Groenlândia)|Danish_Greenlandic_100_|Não disponível|
|Gujarati (Índia)|Indic_General_100_<sup>1</sup>|Indic_General_90_|
|hauçá (Nigéria, Latino)|Latin1_General_100_|Não disponível|
|Híndi (Índia)|Indic_General_100_<sup>1</sup>|Indic_General_90_|
|Igbo (Nigéria)|Latin1_General_100_|Não disponível|
|Inuktitut (Canadá, latino)|Latin1_General_100_|Não disponível|
|Inuktitut (silábico) Canadá|Latin1_General_100_|Não disponível|
|Irlandês (Irlanda)|Latin1_General_100_|Não disponível|
|Japonês (Japão XJIS)|Japanese_XJIS_100_|Japanese_90_, Japanese_|
|Japonês (Japão)|Japanese_Bushu_Kakusu_100_|Não disponível|
|canarim (Índia)|Indic_General_100_<sup>1</sup>|Indic_General_90_|
|Khmer (Camboja)|Khmer_100_<sup>1</sup>|Não disponível|
|Quiché (Guatemala)|Modern_Spanish_100_|Não disponível|
|Quiniaruanda (Ruanda)|Latin1_General_100_|Não disponível|
|Konkani (Índia)|Indic_General_100_<sup>1</sup>|Indic_General_90_|
|Laosiano (RDP do Laos)|Lao_100_<sup>1</sup>|Não disponível|
|Sorábio baixo (Alemanha)|Latin1_General_100_|Não disponível|
|Luxemburguês (Luxemburgo)|Latin1_General_100_|Não disponível|
|Malaiala (Índia)|Indic_General_100_<sup>1</sup>|Não disponível|
|Maltês (Malta)|Maltese_100_|Não disponível|
|Maori (Nova Zelândia)|Maori_100_|Não disponível|
|Mapudungun (Chile)|Mapudungan_100_|Não disponível|
|Marati (Índia)|Indic_General_100_<sup>1</sup>|Indic_General_90_|
|moicano (Canadá)|Mohawk_100_|Não disponível|
|Mongol (RPC)|Cyrillic_General_100_|Não disponível|
|Nepalês (Nepal)|Nepali_100_<sup>1</sup>|Não disponível|
|Norueguês, (Bokmål, Noruega)|Norwegian_100_|Não disponível|
|Norueguês (Nynorsk, Noruega)|Norwegian_100_|Não disponível|
|occitânico (França)|French_100_|Não disponível|
|Odia (Índia)|Indic_General_100_<sup>1</sup>|Não disponível|
|Pashto (Afeganistão)|Pashto_100_<sup>1</sup>|Não disponível|
|Persa (Irã)|Persian_100_|Não disponível|
|panjabi (Índia)|Indic_General_100_<sup>1</sup>|Indic_General_90_|
|Quíchua (Bolívia)|Latin1_General_100_|Não disponível|
|Quíchua (Equador)|Latin1_General_100_|Não disponível|
|Quíchua (Peru)|Latin1_General_100_|Não disponível|
|Romanche (Suíça)|Romansh_100_|Não disponível|
|Sami (Inari, Finlândia)|Sami_Sweden_Finland_100_|Não disponível|
|Sami (Lule, Noruega)|Sami_Norway_100_|Não disponível|
|Sami (Lule, Suécia)|Sami_Sweden_Finland_100_|Não disponível|
|Sami (Norte, Finlândia)|Sami_Sweden_Finland_100_|Não disponível|
|Sami (Norte, Noruega)|Sami_Norway_100_|Não disponível|
|Sami (Norte, Suécia)|Sami_Sweden_Finland_100_|Não disponível|
|Sami (Skolt, Finlândia)|Sami_Sweden_Finland_100_|Não disponível|
|Sami (Sul, Noruega)|Sami_Norway_100_|Não disponível|
|Sami (Sul, Suécia)|Sami_Sweden_Finland_100_|Não disponível|
|Sânscrito (Índia)|Indic_General_100_<sup>1</sup>|Indic_General_90_|
|Sérvio (Bósnia e Herzegovina, cirílico)|Serbian_Cyrillic_100_|Não disponível|
|Sérvio (Bósnia e Herzegovina, latino)|Serbian_Latin_100_|Não disponível|
|Sérvio (Sérvia, cirílico)|Serbian_Cyrillic_100_|Não disponível|
|Sérvio (Sérvia, latino)|Serbian_Latin_100_|Não disponível|
|soto setentrional (África do Sul)|Latin1_General_100_|Não disponível|
|Setswana/Tswana (África do Sul)|Latin1_General_100_|Não disponível|
|Cingalês (Sri Lanka)|Indic_General_100_<sup>1</sup>|Não disponível|
|Suaíle (Quênia)|Latin1_General_100_|Não disponível|
|Siríaco (Síria)|Syriac_100_<sup>1</sup>|Syriac_90_|
|Tadjique (Tadjiquistão)|Cyrillic_General_100_|Não disponível|
|Tamazirte (Argélia, latino)|Tamazight_100_|Não disponível|
|Tâmil (Índia)|Indic_General_100_<sup>1</sup>|Indic_General_90_|
|Télugo (Índia)|Indic_General_100_<sup>1</sup>|Indic_General_90_|
|Tibetano (RPC)|Tibetan_100_<sup>1</sup>|Não disponível|
|Turcomeno (Turcomenistão)|Turkmen_100_|Não disponível|
|Uighur (RPC)|Uighur_100_|Não disponível|
|Sorábio Alto (Alemanha)|Upper_Sorbian_100_|Não disponível|
|Urdu (Paquistão)|Urdu_100_|Não disponível|
|Galês (Reino Unido)|Welsh_100_|Não disponível|
|uolofe (Senegal)|French_100_|Não disponível|
|Xhosa/isiXhosa (África do Sul)|Latin1_General_100_|Não disponível|
|Yakut (Rússia)|Yakut_100_|Não disponível|
|Yi (RPC)|Latin1_General_100_|Não disponível|
|Ioruba (Nigéria)|Latin1_General_100_|Não disponível|
|Zulu/isiZulu (África do Sul)|Latin1_General_100_|Não disponível|
|Preterido, não disponível no nível do servidor no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] nem em versões mais recentes|Híndi|Híndi|
|Preterido, não disponível no nível do servidor no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] nem em versões mais recentes|Korean_Wansung_Unicode|Korean_Wansung_Unicode|
|Preterido, não disponível no nível do servidor no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] nem em versões mais recentes|Lithuanian_Classic|Lithuanian_Classic|
|Preterido, não disponível no nível do servidor no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] nem em versões mais recentes|Macedônio|Macedônio|

<sup>1</sup>Ordenações do Windows somente em Unicode podem ser aplicadas apenas a dados nos níveis de coluna ou de expressão. Eles não podem ser usados como ordenações de banco de dados ou de servidor.

<sup>2</sup>Como o agrupamento de chinês (Taiwan), chinês (RAE de Macau) usa as regras de chinês simplificado; ao contrário do chinês (Taiwan), ele usa a página de código 950.

## <a name="see-also"></a>Consulte Também

- [Suporte a ordenações e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md)
- [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)
- [Constantes](../../t-sql/data-types/constants-transact-sql.md)
- [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?view=sql-server-2017)
- [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)
- [DECLARE @local_variable](../../t-sql/language-elements/declare-local-variable-transact-sql.md)
- [table](../../t-sql/data-types/table-transact-sql.md)
- [sys.fn_helpcollations](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)
