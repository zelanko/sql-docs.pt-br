---
title: Configurações do projeto (mapeamento de tipo) (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: cf426c69-6a8e-4d19-951d-6661d5ae2562
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 7c0866a753bb61cb688ffe491e1de77431ddcb22
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68060157"
---
# <a name="project-settings-type-mapping-db2tosql"></a>Configurações do projeto (mapeamento de tipo) (DB2ToSQL)
A página mapeamento de tipos da caixa de diálogo **configurações do projeto** contém configurações que personalizam como o SSMA converte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] os tipos de dados do DB2 em tipos de dados.  
  
A página mapeamento de tipo está disponível nas caixas de diálogo **configurações do projeto** e **configurações do projeto padrão** .  
  
-   Para especificar configurações para todos os projetos do SSMA futuros, no menu **ferramentas** , clique em **configurações de projeto padrão**, selecione tipo de projeto de migração para o qual as configurações devem ser exibidas ou alteradas no menu suspenso **versão de destino de migração** e clique em mapeamento de **tipo** na parte inferior do painel esquerdo.  
  
-   Para especificar as configurações do projeto atual, no menu **ferramentas** , clique em **configurações do projeto**e, em seguida, clique em mapeamento de **tipo** na parte inferior do painel esquerdo.  
  
Para especificar as configurações do objeto ou da classe de objetos atual, use a guia **mapeamento de tipo** na janela principal do SSMA.  
  
## <a name="options"></a>Opções  
A tabela a seguir mostra as opções da guia **mapeamento de tipos** :  
  
**Tipo de origem**  
O tipo de dados mapeado do DB2.  
  
**Tipo de destino**  
O tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de dados de destino para o tipo de dados do DB2 especificado.  
  
Consulte as tabelas na próxima seção para obter os mapeamentos de tipo do SSMA para DB2 padrão.  
  
**Adicionar**  
Clique para adicionar um tipo de dados à lista de mapeamento.  
  
**Editar**  
Clique para editar o tipo de dados selecionado na lista mapeamento.  
  
**Remover**  
Clique para remover o mapeamento de tipo de dados selecionado da lista de mapeamento.  
  
**Restaurar Padrões**  
Clique para redefinir a lista de mapeamento de tipo para os padrões do SSMA.  
  
## <a name="default-type-mappings"></a>Mapeamentos de tipo padrão  
No SSMA para DB2, você pode definir mapeamentos de tipo personalizados para argumentos, colunas, variáveis locais e valores de retorno. O mapeamento padrão para argumentos e tipos de retorno é quase idêntico.  
  
### <a name="default-argument-type-and-return-value-type-mapping"></a>Tipo de argumento padrão e mapeamento de tipo de valor de retorno  
A tabela a seguir contém o mapeamento de tipo de dados padrão para argumentos e valores de retorno.  
  
|Tipo de dados DB2|Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de dados padrão|  
|-----------------|-------------------------------------------------------------------------|  
|bArquivo|varbinary(max)|  
|binary_double|float [53]|  
|binary_float|float [53]|  
|binary_integer|INT|  
|blob|varbinary(max)|  
|booleano|bit|  
|char|varchar(max)|  
|char varying|varchar(max)|  
|character|varchar(max)|  
|character varying|varchar(max)|  
|CLOB|varchar(max)|  
|date|datetime2 [0]|  
|dec|Dec [38] [0]|  
|decimal|float [53]|  
|double precision|float [53]|  
|FLOAT|float [53]|  
|INT|INT|  
|inteiro|INT|  
|long|varchar(max)|  
|Long RAW|varbinary(max)|  
|Long RAW [\*.. 8000]<sup>\*</sup>|varbinary [\*]|  
|Long RAW [8001..\*]<sup>\*</sup>|varbinary(max)|  
|caractere nacional|nvarchar(max)|  
|variação de caractere nacional|nvarchar(max)|  
|caractere nacional|nvarchar(max)|  
|variação de caractere nacional<sup>\*\*</sup>|nvarchar(max)|  
|variação de caractere nacional<sup>\*</sup>|nvarchar(max)|  
|NCHAR|nvarchar(max)|  
|NCLOB|nvarchar(max)|  
|número|float [53]|  
|numeric|float [53]|  
|nvarchar2|nvarchar(max)|  
|pls_integer|INT|  
|raw|varbinary(max)|  
|real|float [53]|  
|ROWID|UNIQUEIDENTIFIER|  
|sinal de|SMALLINT|  
|SMALLINT|SMALLINT|  
|cadeia de caracteres|varchar(max)|  
|timestamp|datetime2|  
|carimbo de data/hora com fuso horário local|datetimeoffset|  
|carimbo de data/hora com fuso horário|datetimeoffset|  
|UROWID|UNIQUEIDENTIFIER|  
|varchar|varchar(max)|  
|VARCHAR2|varchar(max)|  
|XmlType|Xml|  
  
<sup>\*</sup>Aplica-se somente ao mapeamento de tipo de valor de retorno.  
  
<sup>\*\*</sup>Aplica-se somente ao mapeamento de tipo de argumento.  
  
### <a name="default-column-type-mapping"></a>Mapeamento de tipo de coluna padrão  
A tabela a seguir contém o mapeamento de tipo padrão para colunas.  
  
|Tipo de dados DB2|Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de dados padrão|  
|-----------------|-------------------------------------------------------------------------|  
|bArquivo|varbinary(max)|  
|binary_double|float [53]|  
|binary_float|float [53]|  
|blob|varbinary(max)|  
|char|char|  
|variável de caractere\*[.. \*]|varchar [\*]|  
|Char [\*.. \*]|Char [\*]|  
|character|char|  
|variável de caractere\*[.. \*]|varchar [\*]|  
|caractere [\*.. \*]|Char [\*]|  
|CLOB|varchar(max)|  
|date|datetime2 [0]|  
|dec|Dec [38] [0]|  
|Dec [\*.. \*]|Dec [\*] [0]|  
|Dec [\*.. \*][\*.. \*]|Dec [\*] [\*]|  
|decimal|Decimal [38] [0]|  
|Decimal [\*.. \*]|Decimal [\*] [0]|  
|Decimal [\*.. \*][\*.. \*]|Decimal [\*] [\*]|  
|double precision|float [53]|  
|FLOAT|float [53]|  
|float [\*.. 53]|float [\*]|  
|float [54..\*]|float [53]|  
|INT|INT|  
|inteiro|INT|  
|long|varchar(max)|  
|Long RAW|varbinary(max)|  
|Long RAW [\*.. 8000]|varbinary [\*]|  
|Long RAW [8001..\*]|varbinary(max)|  
|long varchar|varchar(max)|  
|longo [\*.. 8000]|varchar [\*]|  
|longo [8001..\*]|varchar(max)|  
|caractere nacional|NCHAR|  
|variação de caractere nacional\*[.. \*]|nvarchar [\*]|  
|caractere nacional [\*.. \*]|nchar [\*]|  
|caractere nacional|NCHAR|  
|variação de caractere nacional\*[.. \*]|nvarchar [\*]|  
|caractere nacional [\*.. \*]|nchar [\*]|  
|NCHAR|NCHAR|  
|nchar [\*]|nchar [\*]|  
|NCLOB|nvarchar(max)|  
|número|float [53]|  
|número [\*.. \*]|numeric [\*]|  
|número [\*.. \*][\*.. \*]|numeric [\*] [\*]|  
|numeric|numeric|  
|numérico [\*.. \*]|numeric [\*]|  
|numérico [\*.. \*][\*.. \*]|numeric [\*] [\*]|  
|NVARCHAR2 [\*.. \*]|nvarchar [\*]|  
|RAW [\*.. \*]|varbinary [\*]|  
|real|float [53]|  
|ROWID|UNIQUEIDENTIFIER|  
|SMALLINT|SMALLINT|  
|timestamp|datetime2|  
|carimbo de data/hora com fuso horário local|datetimeoffset|  
|carimbo de data/hora com\*fuso horário local [.. \*]|DateTimeOffset [\*]|  
|carimbo de data/hora com fuso horário|datetimeoffset|  
|carimbo de data/hora\*com fuso horário [.. \*]|DateTimeOffset [\*]|  
|carimbo de\*data/hora [.. \*]|datetime2 [\*]|  
|UROWID|UNIQUEIDENTIFIER|  
|UROWID [\*.. \*]|UNIQUEIDENTIFIER|  
|varchar [\*.. \*]|varchar [\*]|  
|VARCHAR2 [\*.. \*]|varchar [\*]|  
|XmlType|Xml|  
  
### <a name="default-local-variable-type-mapping"></a>Mapeamento de tipo de variável local padrão  
A tabela a seguir contém o mapeamento de tipo padrão para variáveis locais.  
  
|Tipo de dados DB2|Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de dados padrão|  
|-----------------|-------------------------------------------------------------------------|  
|Bfile|varbinary(max)|  
|binary_double|float [53]|  
|binary_float|float [53]|  
|binary_interger|INT|  
|Blob|varbinary(max)|  
|Boolean|bit|  
|Char|char|  
|variável de caractere\*[.. 8000]|varchar [\*]|  
|variação de caractere [8001.\*.]|varchar(max)|  
|Char [\*.. 8000]|Char [\*]|  
|Char [8001..\*]|varchar(max)|  
|Caractere|char|  
|variável de caractere\*[.. 8000]|varchar [\*]|  
|variável de caractere [8001.\*.]|varchar(max)|  
|caractere [\*.. 8000]|Char [\*]|  
|caractere [8001..\*]|varchar(max)|  
|CLOB|varchar(max)|  
|date|datetime2 [0]|  
|dec|Dec [38] [0]|  
|Dec [\*.. \*]|Dec [\*] [0]|  
|Dec [\*.. \*][\*.. \*]|Dec [\*] [\*]|  
|decimal|Decimal [38] [0]|  
|Decimal [\*.. \*]|Decimal [\*] [0]|  
|Decimal [\*.. \*][\*.. \*]|Decimal [\*] [\*]|  
|double precision|float [53]|  
|Float|float [53]|  
|float [\*.. 53]|float [\*]|  
|float [54..\*]|float [53]|  
|Int|INT|  
|Integer|INT|  
|inteiro [\*.. \*]|numeric [\*] [0]|  
|long|varchar(max)|  
|Long RAW|varbinary(max)|  
|Long RAW [\*.. 8000]|varbinary [\*]|  
|Long RAW [8001..\*]|varbinary(max)|  
|caractere nacional|NCHAR|  
|variação de caractere nacional\*[.. 4000]|nvarchar [\*]|  
|variação de caractere nacional [4001.\*.]|nvarchar(max)|  
|caractere nacional [\*.. 4000]|nchar [\*]|  
|caractere nacional [4001..\*]|nvarchar(max)|  
|caractere nacional|NCHAR|  
|caractere nacional [\*.. 4000]|nvarchar [\*]|  
|caractere nacional [4001..\*]|nvarchar(max)|  
|variação de caractere nacional\*[.. 4000]|nvarchar [\*]|  
|variação de caractere nacional [4001.\*.]|nvarchar(max)|  
|Nchar|NCHAR|  
|nchar [\*.. 4000]|nchar [\*]|  
|nchar [4001..\*]|nvarchar(max)|  
|nchar variando\*[.. 4000]|nvarchar [\*]|  
|variável nchar [4001..\*]|nvarchar(max)|  
|NCLOB|nvarchar(max)|  
|Número|float [53]|  
|número [\*.. \*]|numeric [\*]|  
|número [\*.. \*][\*.. \*]|numeric [\*] [\*]|  
|Numérico|numeric [38] [0]|  
|numérico [\*.. \*]|numeric [\*]|  
|numérico [\*.. \*][\*.. \*]|numeric [\*] [\*]|  
|NVARCHAR2 [\*.. 4000]|nvarchar [\*]|  
|NVARCHAR2 [4001..\*]|nvarchar(max)|  
|pls_integer|INT|  
|RAW [\*.. 8000]|varbinary [\*]|  
|RAW [8001..\*]|varbinary(max)|  
|Real|float [53]|  
|Rowid|UNIQUEIDENTIFIER|  
|Sinal de|SMALLINT|  
|Smallint|SMALLINT|  
|Cadeia de\*caracteres [.. 8000]|varchar [\*]|  
|Cadeia de caracteres [8001\*..]|varchar(max)|  
|timestamp|datetime2|  
|carimbo de data/hora com fuso horário local|datetimeoffset|  
|carimbo de data/hora com fuso horário|datetimeoffset|  
|carimbo de data/hora com\*fuso horário local [.. \*]|DateTimeOffset [\*]|  
|carimbo de data/hora\*com fuso horário [.. \*]|DateTimeOffset [\*]|  
|carimbo de\*data/hora [.. \*]|datetime2 [\*]|  
|UROWID|UNIQUEIDENTIFIER|  
|UROWID [\*.. \*]|UNIQUEIDENTIFIER|  
|varchar [\*.. 8000]|varchar [\*]|  
|varchar [8001..\*]|varchar(max)|  
|VARCHAR2 [\*.. 8000]|varchar [\*]|  
|VARCHAR2 [8001..\*]|varcha (máx.)|  
|XmlType|Xml|  
  
## <a name="see-also"></a>Consulte Também  
[Referência da interface do usuário &#40;DB2ToSQL&#41;](../../ssma/db2/user-interface-reference-db2tosql.md)  
  
