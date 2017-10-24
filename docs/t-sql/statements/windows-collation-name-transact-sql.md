---
title: Nome de agrupamento do Windows (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Windows collations [SQL Server]
- names [SQL Server], collations
- collations [SQL Server], Windows collations
- Collation Designator
ms.assetid: acceef84-2c68-46e2-a021-be019b7ab14e
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7898592af503300cb1bea261d8809a81fa568155
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="windows-collation-name-transact-sql"></a>Nome de agrupamento do Windows (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Especifica o nome de agrupamento do Windows na cláusula COLLATE em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O nome de agrupamento do Windows é composto pelo designador de agrupamento e pelos estilos de comparação.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<Windows_collation_name> :: =   
CollationDesignator_<ComparisonStyle>  
  
<ComparisonStyle> :: =   
{ CaseSensitivity_AccentSensitivity  [ _KanatypeSensitive ] [ _WidthSensitive ]    
}  
| { _BIN | _BIN2 }  
```  
  
## <a name="arguments"></a>Argumentos  
 *CollationDesignator*  
 Especifica as regras de agrupamento básicas usadas pelo agrupamento do Windows. As regras de agrupamento básicas abrangem o seguinte:  
  
-   As regras de classificação que são aplicadas quando a classificação do dicionário é especificada. As regras de classificação são baseadas no alfabeto ou no idioma.  
  
-   A página de código usada para armazenar dados de caractere não Unicode.  
  
 Alguns exemplos são:  
  
-   Latin1_General ou francês: ambos usam página de código 1252.  
  
-   Turco: usa página de código 1254.  
  
 *Propriedades CaseSensitivity*  
 **CI** Especifica maiusculas de minúsculas, **CS** Especifica diferencia maiusculas de minúsculas.  
  
 *AccentSensitivity*  
 **AI** Especifica diferenciação de acentos, **AS** Especifica acentos.  
  
 *KanatypeSensitive*  
 **Omitido** especifica não diferencia caracteres kana, **KS** Especifica kana.  
  
 *WidthSensitivity*  
 **Omitido** Especifica diferenciação de largura, **WS** Especifica diferenciação de largura.  
  
 **BIN**  
 Especifica a ordem de classificação binária compatível com versões anteriores que será usada.  
  
 **BIN2**  
 Especifica a ordem de classificação binária que usa semântica de comparação de ponto de código.  
  
## <a name="remarks"></a>Comentários  
 Dependendo da versão do agrupamento, alguns pontos de código podem estar indefinidos. Por exemplo, compare:  
  
```  
SELECT LOWER(nchar(504) COLLATE Latin1_General_CI_AS);   
SELECT LOWER (nchar(504) COLLATE Latin1_General_100_CI_AS);  
GO  
```  
  
 A primeira linha retorna um caractere em letra maiúscula quando o agrupamento é Latin1_General_CI_AS, porque este ponto de código é indefinido neste agrupamento.  
  
 Ao trabalhar com alguns idiomas, pode ser crítico evitar agrupamentos mais antigos. Por exemplo, isso se aplica ao télugu.  
  
 Em alguns casos, os agrupamentos do Windows e agrupamentos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem gerar diferentes planos de consulta para a mesma consulta.  
  
## <a name="examples"></a>Exemplos  
 A seguir estão alguns exemplos de nomes de agrupamento do Windows:  
  
-   **Latin1_General_100_**  
  
 O agrupamento usa as regras de classificação do dicionário Latin1 Geral, página de código 1252. Não diferencia maiúsculas de minúsculas e diferencia acento. O agrupamento usa as regras de classificação do dicionário Latin1 Geral e é mapeado para a página de código 1252. Mostrará o número de versão do agrupamento se for um agrupamento do Windows: _90 ou _100. Não diferencia maiúsculas de minúsculas (CI) e diferencia acento (AS).  
  
-   **Estonian_CS_AS**  
  
     O agrupamento usa as regras de classificação do dicionário estoniano, página de código 1257. Diferencia maiúsculas de minúsculas e diferencia acento.  
  
-   **Latin1_General_BIN**  
  
     O agrupamento usa página de código 1252 e regras de classificação binárias. As regras de classificação do dicionário Latin1 Geral são ignoradas.  
  
## <a name="windows-collations"></a>Agrupamentos do Windows  
 Para listar os agrupamentos do Windows suportados pela instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], execute a seguinte consulta.  
  
```  
SELECT * FROM sys.fn_helpcollations() WHERE name NOT LIKE 'SQL%';  
```  
  
 A tabela a seguir lista todos os agrupamentos do Windows com suporte no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
|Localidade do Windows|Agrupamento versão 100|Agrupamento versão 90|  
|--------------------|---------------------------|--------------------------|  
|Alsaciano (França)|Latin1_General_100_|Não disponível|  
|Amárico (Etiópia)|Latin1_General_100_|Não disponível|  
|Armênio (Armênia)|Cyrillic_General_100_|Não disponível|  
|Assamês (Índia)|Assamese_100_ <sup>1</sup>|Não disponível|  
|Bashkir (Rússia)|Bashkir_100_|Não disponível|  
|Basco (País Basco)|Latin1_General_100_|Não disponível|  
|Bengali (Bangladesh)|Bengali_100_<sup>1</sup>|Não disponível|  
|Bengali (India)|Bengali_100_<sup>1</sup>|Não disponível|  
|Bósnio (Bósnia e Herzegovina, Cirílico)|Bosnian_Cyrillic_100_|Não disponível|  
|Bósnio (Bósnia e Herzegovina, Latino)|Bosnian_Latin_100_|Não disponível|  
|Bretão (França)|Breton_100_|Não disponível|  
|Chinese (Macao SAR)|Chinese_Traditional_Pinyin_100_|Não disponível|  
|Chinese (Macao SAR)|Chinese_Traditional_Stroke_Order_100_|Não disponível|  
|Chinese (Singapore)|Chinese_Simplified_Stroke_Order_100_|Não disponível|  
|Corso (França)|Corsican_100_|Não disponível|  
|Croata (Bósnia e Herzegovina, Latino)|Croatian_100_|Não disponível|  
|Dari (Afeganistão)|Dari_100_|Não disponível|  
|Inglês (Índia)|Latin1_General_100_|Não disponível|  
|Inglês (Malásia)|Latin1_General_100_|Não disponível|  
|Inglês (Cingapura)|Latin1_General_100_|Não disponível|  
|Filipino (Filipinas)|Latin1_General_100_|Não disponível|  
|Frisão (Holanda)|Frisian_100_|Não disponível|  
|Georgiano (Geórgia)|Cyrillic_General_100_|Não disponível|  
|Groenlandês (Groenlândia)|Danish_Greenlandic_100_|Não disponível|  
|Gujarati (Índia)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|Hausa (Nigéria, Latino)|Latin1_General_100_|Não disponível|  
|Híndi (Índia)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|Igbo (Nigéria)|Latin1_General_100_|Não disponível|  
|Inuktitut (Canadá, latino)|Latin1_General_100_|Não disponível|  
|Inuktitut (silábico) Canadá|Latin1_General_100_|Não disponível|  
|Irlandês (Irlanda)|Latin1_General_100_|Não disponível|  
|Japonês (Japão XJIS)|Japanese_XJIS_100_|Japanese_90_, Japanese_|  
|Japonês (Japão)|Japanese_Bushu_Kakusu_100_|Não disponível|  
|Kannada (Índia)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
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
|Mohawk (Canadá)|Mohawk_100_|Não disponível|  
|Mongol (RPC)|Cyrillic_General_100_|Não disponível|  
|Nepalês (Nepal)|Nepali_100_<sup>1</sup>|Não disponível|  
|Norueguês (Bokmål, Noruega)|Norwegian_100_|Não disponível|  
|Norueguês (Nynorsk, Noruega)|Norwegian_100_|Não disponível|  
|Occitano (França)|French_100_|Não disponível|  
|Oriá (Índia)|Indic_General_100_<sup>1</sup>|Não disponível|  
|Pashto (Afeganistão)|Pashto_100_<sup>1</sup>|Não disponível|  
|Persa (Irã)|Persian_100_|Não disponível|  
|Punjabi (Índia)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
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
|Sesotho sa Leboa/Sotho do Norte (África do Sul)|Latin1_General_100_|Não disponível|  
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
|Uólofe (Senegal)|French_100_|Não disponível|  
|Xhosa/isiXhosa (África do Sul)|Latin1_General_100_|Não disponível|  
|Yakut (Rússia)|Yakut_100_|Não disponível|  
|Yi (RPC)|Latin1_General_100_|Não disponível|  
|Ioruba (Nigéria)|Latin1_General_100_|Não disponível|  
|Zulu/isiZulu (África do Sul)|Latin1_General_100_|Não disponível|  
|Preterido, não disponível no nível do servidor no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] nem em versões mais recentes|Híndi|Híndi|  
|Preterido, não disponível no nível do servidor no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] nem em versões mais recentes|Korean_Wansung_Unicode|Korean_Wansung_Unicode|  
|Preterido, não disponível no nível do servidor no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] nem em versões mais recentes|Lithuanian_Classic|Lithuanian_Classic|  
|Preterido, não disponível no nível do servidor no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] nem em versões mais recentes|Macedônio|Macedônio|  
  
 <sup>1</sup>agrupamentos do Windows somente Unicode só podem ser aplicados aos dados de nível de coluna ou expressão. Eles não podem ser usados como agrupamentos de banco de dados ou de servidor.  
  
 <sup>2</sup>como o agrupamento de chinês (Taiwan), chinês (Macau) usa as regras de chinês simplificado; ao contrário do chinês (Taiwan), ele usa a página de código 950.  
  
## <a name="see-also"></a>Consulte também  
 [Suporte a agrupamentos e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [Constantes &#40; Transact-SQL &#41;](../../t-sql/data-types/constants-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [tabela &#40; Transact-SQL &#41;](../../t-sql/data-types/table-transact-sql.md)   
 [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)  
  
  

