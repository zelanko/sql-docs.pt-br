---
title: "Configurações (mapeamento de tipo) do projeto (OracleToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4bb8466e-2199-4f00-8513-b04e9586723d
caps.latest.revision: "8"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: f4be0d12ce3067f46c934cfa7e053ddd1779ac9f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="project-settings-type-mapping-oracletosql"></a>Configurações (mapeamento de tipo) do projeto (OracleToSQL)
A página mapeamento de tipo do **configurações de projeto** caixa de diálogo contém configurações que personalizam como o SSMA converte tipos de dados Oracle em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de dados.  
  
A mapeamento de tipo de página está disponível na **configurações de projeto** e **configurações de projeto padrão** caixas de diálogo.  
  
-   Para especificar configurações para todos os projetos futuros do SSMA, no **ferramentas** menu clique **configurações de projeto padrão**, selecione o tipo de projeto de migração para o qual as configurações são necessárias para ser exibido ou alterado de **versão de destino de migração** lista suspensa e, em seguida, clique em **mapeamento de tipo** na parte inferior do painel esquerdo.  
  
-   Para especificar as configurações para o projeto atual, no **ferramentas** menu clique **configurações de projeto**e, em seguida, clique em **mapeamento de tipo** na parte inferior do painel esquerdo.  
  
Para especificar configurações para o objeto atual ou a classe de objetos, use o **mapeamento de tipo** guia na janela principal do SSMA.  
  
## <a name="options"></a>Opções  
A tabela a seguir mostra o **mapeamento de tipo** opções da guia:  
  
**Tipo de Origem**  
O tipo de dados Oracle mapeado.  
  
**Tipo de destino**  
O destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipo de dados para o tipo de dados especificado do Oracle.  
  
Consulte as tabelas na próxima seção para o padrão do SSMA para mapeamentos de tipo Oracle.  
  
**Adicionar**  
Clique para adicionar um tipo de dados para a lista de mapeamento.  
  
**Editar**  
Clique para editar o tipo de dados selecionado na lista de mapeamento.  
  
**Remover**  
Clique para remover o mapeamento de tipo de dados selecionado da lista de mapeamento.  
  
**Redefinir para padrão**  
Clique para redefinir a lista de mapeamento de tipo para os padrões do SSMA.  
  
## <a name="default-type-mappings"></a>Mapeamentos de tipo padrão  
SSMA para Oracle, você pode definir mapeamentos de tipo personalizado para argumentos, colunas, variáveis locais e valores de retorno. O mapeamento padrão para argumentos e tipos de retorno é quase idêntico.  
  
### <a name="default-argument-type-and-return-value-type-mapping"></a>Tipo de argumento padrão e mapeamento de tipo de valor de retorno  
A tabela a seguir contém o mapeamento de tipo de dados padrão para argumentos e valores de retorno.  
  
|Tipo de dados Oracle|Padrão [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipo de dados|  
|--------------------|-------------------------------------------------------------------------|  
|BFILE|varbinary(max)|  
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
|Data|datetime2 [0]|  
|dec|DEC [38] [0]|  
|Decimal|float [53]|  
|precisão dupla|float [53]|  
|FLOAT|float [53]|  
|INT|INT|  
|inteiro|INT|  
|long|varchar(max)|  
|Long raw|varbinary(max)|  
|Long raw [\*... 8000]<sup>*</sup>|varbinary [*]|  
|Long raw [8001...\*]<sup>*</sup>|varbinary(max)|  
|National char|nvarchar(max)|  
|variável de caractere nacional|nvarchar(max)|  
|caracteres nacionais|nvarchar(max)|  
|variável de caracteres nacionais<sup>**</sup>|nvarchar(max)|  
|variável de caracteres nacionais<sup>*</sup>|nvarchar(max)|  
|NCHAR|nvarchar(max)|  
|NCLOB|nvarchar(max)|  
|number|float [53]|  
|NUMERIC|float [53]|  
|NVARCHAR2|nvarchar(max)|  
|pls_integer|INT|  
|raw|varbinary(max)|  
|REAL|float [53]|  
|RowId|UNIQUEIDENTIFIER|  
|Signtype|SMALLINT|  
|SMALLINT|SMALLINT|  
|cadeia de caracteres|varchar(max)|  
|timestamp|datetime2|  
|carimbo de hora com o fuso horário local|datetimeoffset|  
|carimbo de hora com o fuso horário|datetimeoffset|  
|Urowid|UNIQUEIDENTIFIER|  
|varchar|varchar(max)|  
|VARCHAR2|varchar(max)|  
|Tipo XML|xml|  
  
<sup>*</sup>Aplica-se para retornar o mapeamento de tipo de valor apenas.  
  
<sup>**</sup>Aplica-se ao mapeamento de tipo de argumento somente.  
  
### <a name="default-column-type-mapping"></a>Mapeamento de tipo de coluna padrão  
A tabela a seguir contém o mapeamento de tipo padrão para colunas.  
  
|Tipo de dados Oracle|Padrão [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipo de dados|  
|--------------------|-------------------------------------------------------------------------|  
|BFILE|varbinary(max)|  
|binary_double|float [53]|  
|binary_float|float [53]|  
|blob|varbinary(max)|  
|char|char|  
|variável de char [*... \*]|varchar [*]|  
|char [*... \*]|char [*]|  
|character|char|  
|variável de caractere [*... \*]|varchar [*]|  
|caracteres [*... \*]|char [*]|  
|CLOB|varchar(max)|  
|Data|datetime2 [0]|  
|dec|DEC [38] [0]|  
|DEC [*... \*]|DEC [*] [0]|  
|DEC [*... \*][\*.. \*]|dec[*][\*]|  
|Decimal|decimal [38] [0]|  
|decimal [*... \*]|decimal [*] [0]|  
|decimal [*... \*][\*.. \*]|decimal [*] [\*]|  
|precisão dupla|float [53]|  
|FLOAT|float [53]|  
|float [*... 53]|float [*]|  
|float [54... *]|float [53]|  
|INT|INT|  
|inteiro|INT|  
|long|varchar(max)|  
|Long raw|varbinary(max)|  
|Long raw [*... 8000]|varbinary [*]|  
|Long raw [8001... *]|varbinary(max)|  
|Long varchar|varchar(max)|  
|tempo [*... 8000]|varchar [*]|  
|tempo [8001... *]|varchar(max)|  
|National char|NCHAR|  
|variável de caractere nacional [*... \*]|nvarchar [*]|  
|National char [*... \*]|nchar [*]|  
|caracteres nacionais|NCHAR|  
|variável de caractere nacional [*... \*]|nvarchar [*]|  
|caracteres nacionais [*... \*]|nchar [*]|  
|NCHAR|NCHAR|  
|nchar [*]|nchar [*]|  
|NCLOB|nvarchar(max)|  
|number|float [53]|  
|número [*... \*]|numérico [*]|  
|número [*... \*][\*.. \*]|numérico [*] [\*]|  
|NUMERIC|NUMERIC|  
|numérico [*... \*]|numérico [*]|  
|numérico [*... \*][\*.. \*]|numérico [*] [\*]|  
|NVARCHAR2 [*... \*]|nvarchar [*]|  
|RAW [*... \*]|varbinary [*]|  
|REAL|float [53]|  
|RowId|UNIQUEIDENTIFIER|  
|SMALLINT|SMALLINT|  
|timestamp|datetime2|  
|carimbo de hora com o fuso horário local|datetimeoffset|  
|carimbo de hora com o fuso horário local [*... \*]|DateTimeOffset [*]|  
|carimbo de hora com o fuso horário|datetimeoffset|  
|carimbo de hora com o fuso horário [*... \*]|DateTimeOffset [*]|  
|carimbo de hora [*... \*]|datetime2 [*]|  
|Urowid|UNIQUEIDENTIFIER|  
|urowid [*... \*]|UNIQUEIDENTIFIER|  
|varchar [*... \*]|varchar [*]|  
|VARCHAR2 [*... \*]|varchar [*]|  
|Tipo XML|xml|  
  
### <a name="default-local-variable-type-mapping"></a>Mapeamento de tipo de variável Local padrão  
A tabela a seguir contém o mapeamento de tipo padrão para variáveis locais.  
  
|Tipo de dados Oracle|Padrão [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipo de dados|  
|--------------------|-------------------------------------------------------------------------|  
|BFILE|varbinary(max)|  
|binary_double|float [53]|  
|binary_float|float [53]|  
|binary_interger|INT|  
|Blob|varbinary(max)|  
|Booliano|bit|  
|Char|char|  
|variável de char [*... 8000]|varchar [*]|  
|variável de char [8001... *]|varchar(max)|  
|char [*... 8000]|char [*]|  
|char [8001... *]|varchar(max)|  
|Caractere|char|  
|variável de caractere [*... 8000]|varchar [*]|  
|variável de caractere [8001... *]|varchar(max)|  
|caracteres [*... 8000]|char [*]|  
|caracteres [8001... *]|varchar(max)|  
|CLOB|varchar(max)|  
|Data|datetime2 [0]|  
|dec|DEC [38] [0]|  
|DEC [*... \*]|DEC [*] [0]|  
|DEC [*... \*][\*.. \*]|dec[*][\*]|  
|Decimal|decimal [38] [0]|  
|decimal [*... \*]|decimal [*] [0]|  
|decimal [*... \*][\*.. \*]|decimal [*] [\*]|  
|precisão dupla|float [53]|  
|float|float [53]|  
|float [*... 53]|float [*]|  
|float [54... *]|float [53]|  
|Int|INT|  
|Integer|INT|  
|inteiro [*... \*]|numérico [*] [0]|  
|Longo|varchar(max)|  
|Long raw|varbinary(max)|  
|Long raw [*... 8000]|varbinary [*]|  
|Long raw [8001... *]|varbinary(max)|  
|National char|NCHAR|  
|variável de caractere nacional [*... 4000]|nvarchar [*]|  
|variável de caractere nacional [4001... *]|nvarchar(max)|  
|National char [*... 4000]|nchar [*]|  
|National char [4001... *]|nvarchar(max)|  
|caracteres nacionais|NCHAR|  
|caracteres nacionais [*... 4000]|nvarchar [*]|  
|caracteres nacionais [4001... *]|nvarchar(max)|  
|variável de caractere nacional [*... 4000]|nvarchar [*]|  
|variável de caractere nacional [4001... *]|nvarchar(max)|  
|Nchar|NCHAR|  
|nchar [*... 4000]|nchar [*]|  
|nchar [4001... *]|nvarchar(max)|  
|nchar variados [*... 4000]|nvarchar [*]|  
|nchar variados [4001... *]|nvarchar(max)|  
|NCLOB|nvarchar(max)|  
|Número|float [53]|  
|número [*... \*]|numérico [*]|  
|número [*... \*][\*.. \*]|numérico [*] [\*]|  
|Numérico|numérico [38] [0]|  
|numérico [*... \*]|numérico [*]|  
|numérico [*... \*][\*.. \*]|numérico [*] [\*]|  
|NVARCHAR2 [*... 4000]|nvarchar [*]|  
|NVARCHAR2 [4001... *]|nvarchar(max)|  
|pls_integer|INT|  
|RAW [*... 8000]|varbinary [*]|  
|RAW [8001... *]|varbinary(max)|  
|Real|float [53]|  
|RowId|UNIQUEIDENTIFIER|  
|Signtype|SMALLINT|  
|Smallint|SMALLINT|  
|cadeia de caracteres [*... 8000]|varchar [*]|  
|cadeia de caracteres [8001... *]|varchar(max)|  
|timestamp|datetime2|  
|carimbo de hora com o fuso horário local|datetimeoffset|  
|carimbo de hora com o fuso horário|datetimeoffset|  
|carimbo de hora com o fuso horário local [*... \*]|DateTimeOffset [*]|  
|carimbo de hora com o fuso horário [*... \*]|DateTimeOffset [*]|  
|carimbo de hora [*... \*]|datetime2 [*]|  
|Urowid|UNIQUEIDENTIFIER|  
|urowid [*... \*]|UNIQUEIDENTIFIER|  
|varchar [*... 8000]|varchar [*]|  
|varchar [8001... *]|varchar(max)|  
|VARCHAR2 [*... 8000]|varchar [*]|  
|VARCHAR2 [8001... *]|varcha(max)|  
|Tipo XML|xml|  
  
## <a name="see-also"></a>Consulte Também  
[Referência de Interface do usuário &#40; OracleToSQL &#41;](../../ssma/oracle/user-interface-reference-oracletosql.md)  
  
