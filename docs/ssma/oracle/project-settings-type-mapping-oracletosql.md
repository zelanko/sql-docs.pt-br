---
title: Project Settings (Type Mapping) (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4bb8466e-2199-4f00-8513-b04e9586723d
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 449f1ecc2fbcc2f9e18ea24cb5bd42323bbf5ddc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62625880"
---
# <a name="project-settings-type-mapping-oracletosql"></a>Configurações do projeto (mapeamento de tipo) (OracleToSQL)
A página de mapeamento de tipo a **configurações do projeto** caixa de diálogo contém configurações que personalizam como SSMA converte tipos de dados Oracle em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados.  
  
A página mapeamento de tipo está disponível na **configurações do projeto** e **configurações do projeto padrão** caixas de diálogo.  
  
-   Para especificar configurações para todos os projetos futuros do SSMA, na **ferramentas** menu, clique em **configurações do projeto padrão**, selecione o tipo de projeto de migração para o qual as configurações são necessárias para ser exibida ou alterada de **Versão de destino de migração** lista suspensa e, em seguida, clique em **mapeamento de tipo** na parte inferior do painel esquerdo.  
  
-   Para especificar configurações para o projeto atual, nos **ferramentas** menu, clique em **configurações do projeto**e, em seguida, clique em **mapeamento de tipo** na parte inferior do painel esquerdo.  
  
Para especificar configurações para o objeto atual ou a classe de objetos, use o **mapeamento de tipo** guia na janela principal do SSMA.  
  
## <a name="options"></a>Opções  
A tabela a seguir mostra a **mapeamento de tipo** opções da guia:  
  
**Tipo de Origem**  
O tipo de dados Oracle mapeado.  
  
**Tipo de destino**  
O destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados para o tipo de dados Oracle especificado.  
  
Consulte as tabelas na próxima seção para o padrão do SSMA para mapeamentos de tipo Oracle.  
  
**Adicionar**  
Clique para adicionar um tipo de dados à lista de mapeamento.  
  
**Editar**  
Clique para editar o tipo de dados selecionado na lista de mapeamento.  
  
**Remover**  
Clique para remover o mapeamento de tipo de dados selecionado da lista de mapeamento.  
  
**Restaurar Padrões**  
Clique para redefinir a lista de mapeamento de tipo para os padrões do SSMA.  
  
## <a name="default-type-mappings"></a>Mapeamentos de tipo padrão  
No SSMA para Oracle, você pode definir mapeamentos de tipo personalizado de argumentos, colunas, variáveis locais e valores de retorno. O mapeamento padrão para argumentos e tipos de retorno é quase idêntico.  
  
### <a name="default-argument-type-and-return-value-type-mapping"></a>Tipo de argumento padrão e mapeamento de tipo de valor de retorno  
A tabela a seguir contém o mapeamento de tipo de dados padrão para argumentos e valores de retorno.  
  
|Tipo de dados Oracle|Padrão [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados|  
|--------------------|-------------------------------------------------------------------------|  
|BFILE|varbinary(max)|  
|binary_double|float[53]|  
|binary_float|float[53]|  
|binary_integer|INT|  
|blob|varbinary(max)|  
|boolean|bit|  
|char|varchar(max)|  
|char varying|varchar(max)|  
|character|varchar(max)|  
|character varying|varchar(max)|  
|CLOB|varchar(max)|  
|date|datetime2[0]|  
|dec|dec[38][0]|  
|Decimal|float[53]|  
|precisão dupla|float[53]|  
|float|float[53]|  
|INT|INT|  
|inteiro|INT|  
|long|varchar(max)|  
|Long raw|varbinary(max)|  
|Long raw [\*... 8000]<sup>*</sup>|varbinary[*]|  
|Long raw [8001...\*]<sup>*</sup>|varbinary(max)|  
|char nacional|nvarchar(max)|  
|National char variados|nvarchar(max)|  
|caracteres nacionais|nvarchar(max)|  
|variável de caracteres nacionais<sup>**</sup>|nvarchar(max)|  
|variável de caracteres nacionais<sup>*</sup>|nvarchar(max)|  
|NCHAR|nvarchar(max)|  
|NCLOB|nvarchar(max)|  
|number|float[53]|  
|numeric|float[53]|  
|nvarchar2|nvarchar(max)|  
|pls_integer|INT|  
|raw|varbinary(max)|  
|REAL|float[53]|  
|RowId|UNIQUEIDENTIFIER|  
|Signtype|SMALLINT|  
|SMALLINT|SMALLINT|  
|cadeia de caracteres|varchar(max)|  
|timestamp|datetime2|  
|carimbo de hora com fuso horário local|datetimeoffset|  
|carimbo de hora com fuso horário|datetimeoffset|  
|urowid|UNIQUEIDENTIFIER|  
|varchar|varchar(max)|  
|varchar2|varchar(max)|  
|xmltype|xml|  
  
<sup>*</sup> Aplica-se para retornar o mapeamento de tipo de valor apenas.  
  
<sup>**</sup> Aplica-se ao mapeamento de tipo de argumento somente.  
  
### <a name="default-column-type-mapping"></a>Mapeamento de tipo de coluna padrão  
A tabela a seguir contém o mapeamento de tipo padrão para colunas.  
  
|Tipo de dados Oracle|Padrão [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados|  
|--------------------|-------------------------------------------------------------------------|  
|BFILE|varbinary(max)|  
|binary_double|float[53]|  
|binary_float|float[53]|  
|blob|varbinary(max)|  
|char|char|  
|variando de char [*... \*]|varchar[*]|  
|char[*..\*]|char[*]|  
|character|char|  
|a variável de caractere [*... \*]|varchar[*]|  
|caracteres [*... \*]|char[*]|  
|CLOB|varchar(max)|  
|date|datetime2[0]|  
|dec|dec[38][0]|  
|DEC [*... \*]|dec[*][0]|  
|dec[*..\*][\*..\*]|dec[*][\*]|  
|Decimal|decimal[38][0]|  
|decimal[*..\*]|decimal[*][0]|  
|decimal[*..\*][\*..\*]|decimal[*][\*]|  
|precisão dupla|float[53]|  
|float|float[53]|  
|float [*... 53]|float[*]|  
|float[54..*]|float[53]|  
|INT|INT|  
|inteiro|INT|  
|long|varchar(max)|  
|Long raw|varbinary(max)|  
|Long raw [*... 8000]|varbinary[*]|  
|Long raw [8001... *]|varbinary(max)|  
|long varchar|varchar(max)|  
|Long [*... 8000]|varchar[*]|  
|long[8001..*]|varchar(max)|  
|char nacional|NCHAR|  
|National char variados [*... \*]|nvarchar[*]|  
|national char[*..\*]|nchar[*]|  
|caracteres nacionais|NCHAR|  
|a variável de caractere nacional [*... \*]|nvarchar[*]|  
|caractere nacional [*... \*]|nchar[*]|  
|NCHAR|NCHAR|  
|nchar[*]|nchar[*]|  
|NCLOB|nvarchar(max)|  
|number|float[53]|  
|number[*..\*]|numérico [*]|  
|number[*..\*][\*..\*]|numeric[*][\*]|  
|numeric|numeric|  
|numeric[*..\*]|numérico [*]|  
|numeric[*..\*][\*..\*]|numeric[*][\*]|  
|nvarchar2[*..\*]|nvarchar[*]|  
|raw[*..\*]|varbinary[*]|  
|REAL|float[53]|  
|RowId|UNIQUEIDENTIFIER|  
|SMALLINT|SMALLINT|  
|timestamp|datetime2|  
|carimbo de hora com fuso horário local|datetimeoffset|  
|carimbo de hora com fuso horário local [*... \*]|datetimeoffset[*]|  
|carimbo de hora com fuso horário|datetimeoffset|  
|carimbo de hora com fuso horário [*... \*]|datetimeoffset[*]|  
|timestamp[*..\*]|datetime2[*]|  
|urowid|UNIQUEIDENTIFIER|  
|urowid[*..\*]|UNIQUEIDENTIFIER|  
|varchar[*..\*]|varchar[*]|  
|varchar2[*..\*]|varchar[*]|  
|Xmltype|xml|  
  
### <a name="default-local-variable-type-mapping"></a>Mapeamento de tipo de variável Local padrão  
A tabela a seguir contém o mapeamento de tipo padrão para variáveis locais.  
  
|Tipo de dados Oracle|Padrão [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados|  
|--------------------|-------------------------------------------------------------------------|  
|Bfile|varbinary(max)|  
|binary_double|float[53]|  
|binary_float|float[53]|  
|binary_interger|INT|  
|Blob|varbinary(max)|  
|Booliano|bit|  
|Char|char|  
|variando de char [*... 8000]|varchar[*]|  
|char varying[8001..*]|varchar(max)|  
|char[*..8000]|char[*]|  
|char[8001..*]|varchar(max)|  
|Caractere|char|  
|a variável de caractere [*... 8000]|varchar[*]|  
|a variável de caractere [8001... *]|varchar(max)|  
|caracteres [*... 8000]|char[*]|  
|caracteres [8001... *]|varchar(max)|  
|CLOB|varchar(max)|  
|date|datetime2[0]|  
|dec|dec[38][0]|  
|DEC [*... \*]|dec[*][0]|  
|dec[*..\*][\*..\*]|dec[*][\*]|  
|Decimal|decimal[38][0]|  
|decimal[*..\*]|decimal[*][0]|  
|decimal[*..\*][\*..\*]|decimal[*][\*]|  
|precisão dupla|float[53]|  
|float|float[53]|  
|float [*... 53]|float[*]|  
|float[54..*]|float[53]|  
|Int|INT|  
|Integer|INT|  
|inteiro [*... \*]|numeric[*][0]|  
|Longo|varchar(max)|  
|Long raw|varbinary(max)|  
|Long raw [*... 8000]|varbinary[*]|  
|Long raw [8001... *]|varbinary(max)|  
|char nacional|NCHAR|  
|National char variados [*... 4000]|nvarchar[*]|  
|National char variados [4001... *]|nvarchar(max)|  
|National char [*... 4000]|nchar[*]|  
|National char [4001... *]|nvarchar(max)|  
|caracteres nacionais|NCHAR|  
|caractere nacional [*... 4000]|nvarchar[*]|  
|caractere nacional [4001... *]|nvarchar(max)|  
|a variável de caractere nacional [*... 4000]|nvarchar[*]|  
|a variável de caractere nacional [4001... *]|nvarchar(max)|  
|Nchar|NCHAR|  
|nchar[*..4000]|nchar[*]|  
|nchar[4001..*]|nvarchar(max)|  
|nchar variados [*... 4000]|nvarchar[*]|  
|nchar varying [4001..*]|nvarchar(max)|  
|NCLOB|nvarchar(max)|  
|Number|float[53]|  
|number[*..\*]|numérico [*]|  
|number[*..\*][\*..\*]|numeric[*][\*]|  
|Numeric|numeric[38][0]|  
|numeric[*..\*]|numérico [*]|  
|numeric[*..\*][\*..\*]|numeric[*][\*]|  
|nvarchar2[*..4000]|nvarchar[*]|  
|nvarchar2[4001..*]|nvarchar(max)|  
|pls_integer|INT|  
|RAW [*... 8000]|varbinary[*]|  
|raw[8001..*]|varbinary(max)|  
|Real|float[53]|  
|Rowid|UNIQUEIDENTIFIER|  
|Signtype|SMALLINT|  
|Smallint|SMALLINT|  
|cadeia de caracteres [*... 8000]|varchar[*]|  
|string[8001..*]|varchar(max)|  
|timestamp|datetime2|  
|carimbo de hora com fuso horário local|datetimeoffset|  
|carimbo de hora com fuso horário|datetimeoffset|  
|carimbo de hora com fuso horário local [*... \*]|datetimeoffset[*]|  
|carimbo de hora com fuso horário [*... \*]|datetimeoffset[*]|  
|timestamp[*..\*]|datetime2[*]|  
|urowid|UNIQUEIDENTIFIER|  
|urowid[*..\*]|UNIQUEIDENTIFIER|  
|varchar[*..8000]|varchar[*]|  
|varchar[8001..*]|varchar(max)|  
|varchar2[*..8000]|varchar[*]|  
|varchar2[8001..*]|varcha(max)|  
|Xmltype|xml|  
  
## <a name="see-also"></a>Consulte também  
[Referência da Interface do usuário &#40;OracleToSQL&#41;](../../ssma/oracle/user-interface-reference-oracletosql.md)  
  
