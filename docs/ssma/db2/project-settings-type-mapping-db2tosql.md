---
title: Configurações (mapeamento de tipo) do projeto (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: cf426c69-6a8e-4d19-951d-6661d5ae2562
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: e6c81fab41d0e6d25ad442c8856b15edacf63b39
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="project-settings-type-mapping-db2tosql"></a>Configurações (mapeamento de tipo) do projeto (DB2ToSQL)
A página mapeamento de tipo do **configurações de projeto** caixa de diálogo contém configurações que personalizam como o SSMA converte tipos de dados do DB2 em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de dados.  
  
A mapeamento de tipo de página está disponível na **configurações de projeto** e **configurações de projeto padrão** caixas de diálogo.  
  
-   Para especificar configurações para todos os projetos futuros do SSMA, no **ferramentas** menu clique **configurações de projeto padrão**, selecione o tipo de projeto de migração para o qual as configurações são necessárias para ser exibido ou alterado de **versão de destino de migração** lista suspensa e, em seguida, clique em **mapeamento de tipo** na parte inferior do painel esquerdo.  
  
-   Para especificar as configurações para o projeto atual, no **ferramentas** menu clique **configurações de projeto**e, em seguida, clique em **mapeamento de tipo** na parte inferior do painel esquerdo.  
  
Para especificar configurações para o objeto atual ou a classe de objetos, use o **mapeamento de tipo** guia na janela principal do SSMA.  
  
## <a name="options"></a>Opções  
A tabela a seguir mostra o **mapeamento de tipo** opções da guia:  
  
**Tipo de Origem**  
O tipo de dados DB2 mapeado.  
  
**Tipo de destino**  
O destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipo de dados para o tipo de dados do DB2 especificado.  
  
Consulte as tabelas na próxima seção para o padrão do SSMA para mapeamentos de tipo DB2.  
  
**Adicionar**  
Clique para adicionar um tipo de dados para a lista de mapeamento.  
  
**Editar**  
Clique para editar o tipo de dados selecionado na lista de mapeamento.  
  
**Remover**  
Clique para remover o mapeamento de tipo de dados selecionado da lista de mapeamento.  
  
**Redefinir para padrão**  
Clique para redefinir a lista de mapeamento de tipo para os padrões do SSMA.  
  
## <a name="default-type-mappings"></a>Mapeamentos de tipo padrão  
SSMA para DB2, você pode definir mapeamentos de tipo personalizado para argumentos, colunas, variáveis locais e valores de retorno. O mapeamento padrão para argumentos e tipos de retorno é quase idêntico.  
  
### <a name="default-argument-type-and-return-value-type-mapping"></a>Tipo de argumento padrão e mapeamento de tipo de valor de retorno  
A tabela a seguir contém o mapeamento de tipo de dados padrão para argumentos e valores de retorno.  
  
|DB2 Tipo de dados|Padrão [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipo de dados|  
|-----------------|-------------------------------------------------------------------------|  
|BFILE|varbinary(max)|  
|binary_double|float [53]|  
|binary_float|float [53]|  
|binary_integer|int|  
|blob|varbinary(max)|  
|booleano|bit|  
|char|varchar(max)|  
|char varying|varchar(max)|  
|character|varchar(max)|  
|character varying|varchar(max)|  
|CLOB|varchar(max)|  
|date|datetime2[0]|  
|dec|dec[38][0]|  
|Decimal|float [53]|  
|precisão dupla|float [53]|  
|float|float [53]|  
|int|int|  
|inteiro|int|  
|long|varchar(max)|  
|Long raw|varbinary(max)|  
|Long raw [\*... 8000]<sup>*</sup>|varbinary[*]|  
|Long raw [8001...\*]<sup>*</sup>|varbinary(max)|  
|National char|nvarchar(max)|  
|variável de caractere nacional|nvarchar(max)|  
|caracteres nacionais|nvarchar(max)|  
|variável de caracteres nacionais<sup>**</sup>|nvarchar(max)|  
|variável de caracteres nacionais<sup>*</sup>|nvarchar(max)|  
|NCHAR|nvarchar(max)|  
|NCLOB|nvarchar(max)|  
|number|float [53]|  
|numeric|float [53]|  
|NVARCHAR2|nvarchar(max)|  
|pls_integer|int|  
|raw|varbinary(max)|  
|real|float [53]|  
|RowId|uniqueidentifier|  
|Signtype|smallint|  
|smallint|smallint|  
|cadeia de caracteres|varchar(max)|  
|timestamp|datetime2|  
|carimbo de hora com o fuso horário local|datetimeoffset|  
|carimbo de hora com o fuso horário|datetimeoffset|  
|Urowid|uniqueidentifier|  
|varchar|varchar(max)|  
|VARCHAR2|varchar(max)|  
|Tipo XML|xml|  
  
<sup>*</sup> Aplica-se para retornar o mapeamento de tipo de valor apenas.  
  
<sup>**</sup> Aplica-se ao mapeamento de tipo de argumento somente.  
  
### <a name="default-column-type-mapping"></a>Mapeamento de tipo de coluna padrão  
A tabela a seguir contém o mapeamento de tipo padrão para colunas.  
  
|DB2 Tipo de dados|Padrão [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipo de dados|  
|-----------------|-------------------------------------------------------------------------|  
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
|date|datetime2[0]|  
|dec|dec[38][0]|  
|DEC [*... \*]|dec[*][0]|  
|DEC [*... \*][\*.. \*]|dec[*][\*]|  
|Decimal|decimal[38][0]|  
|decimal [*... \*]|decimal[*][0]|  
|decimal [*... \*][\*.. \*]|decimal[*][\*]|  
|precisão dupla|float [53]|  
|float|float [53]|  
|float [*... 53]|float[*]|  
|float [54... *]|float [53]|  
|int|int|  
|inteiro|int|  
|long|varchar(max)|  
|Long raw|varbinary(max)|  
|Long raw [*... 8000]|varbinary[*]|  
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
|número [*... \*][\*.. \*]|numeric[*][\*]|  
|numeric|numeric|  
|numérico [*... \*]|numérico [*]|  
|numérico [*... \*][\*.. \*]|numeric[*][\*]|  
|NVARCHAR2 [*... \*]|nvarchar [*]|  
|RAW [*... \*]|varbinary[*]|  
|real|float [53]|  
|RowId|uniqueidentifier|  
|smallint|smallint|  
|timestamp|datetime2|  
|carimbo de hora com o fuso horário local|datetimeoffset|  
|carimbo de hora com o fuso horário local [*... \*]|datetimeoffset[*]|  
|carimbo de hora com o fuso horário|datetimeoffset|  
|carimbo de hora com o fuso horário [*... \*]|datetimeoffset[*]|  
|carimbo de hora [*... \*]|datetime2[*]|  
|Urowid|uniqueidentifier|  
|urowid [*... \*]|uniqueidentifier|  
|varchar [*... \*]|varchar [*]|  
|VARCHAR2 [*... \*]|varchar [*]|  
|Tipo XML|xml|  
  
### <a name="default-local-variable-type-mapping"></a>Mapeamento de tipo de variável Local padrão  
A tabela a seguir contém o mapeamento de tipo padrão para variáveis locais.  
  
|DB2 Tipo de dados|Padrão [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipo de dados|  
|-----------------|-------------------------------------------------------------------------|  
|BFILE|varbinary(max)|  
|binary_double|float [53]|  
|binary_float|float [53]|  
|binary_interger|int|  
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
|date|datetime2[0]|  
|dec|dec[38][0]|  
|DEC [*... \*]|dec[*][0]|  
|DEC [*... \*][\*.. \*]|dec[*][\*]|  
|Decimal|decimal[38][0]|  
|decimal [*... \*]|decimal[*][0]|  
|decimal [*... \*][\*.. \*]|decimal[*][\*]|  
|precisão dupla|float [53]|  
|Valor Flutuante|float [53]|  
|float [*... 53]|float[*]|  
|float [54... *]|float [53]|  
|Int|int|  
|Integer|int|  
|inteiro [*... \*]|numeric[*][0]|  
|Longo|varchar(max)|  
|Long raw|varbinary(max)|  
|Long raw [*... 8000]|varbinary[*]|  
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
|número [*... \*][\*.. \*]|numeric[*][\*]|  
|Numérico|numeric[38][0]|  
|numérico [*... \*]|numérico [*]|  
|numérico [*... \*][\*.. \*]|numeric[*][\*]|  
|NVARCHAR2 [*... 4000]|nvarchar [*]|  
|NVARCHAR2 [4001... *]|nvarchar(max)|  
|pls_integer|int|  
|RAW [*... 8000]|varbinary[*]|  
|RAW [8001... *]|varbinary(max)|  
|Real|float [53]|  
|RowId|uniqueidentifier|  
|Signtype|smallint|  
|Smallint|smallint|  
|cadeia de caracteres [*... 8000]|varchar [*]|  
|cadeia de caracteres [8001... *]|varchar(max)|  
|timestamp|datetime2|  
|carimbo de hora com o fuso horário local|datetimeoffset|  
|carimbo de hora com o fuso horário|datetimeoffset|  
|carimbo de hora com o fuso horário local [*... \*]|datetimeoffset[*]|  
|carimbo de hora com o fuso horário [*... \*]|datetimeoffset[*]|  
|carimbo de hora [*... \*]|datetime2[*]|  
|Urowid|uniqueidentifier|  
|urowid [*... \*]|uniqueidentifier|  
|varchar [*... 8000]|varchar [*]|  
|varchar [8001... *]|varchar(max)|  
|VARCHAR2 [*... 8000]|varchar [*]|  
|VARCHAR2 [8001... *]|varcha(max)|  
|Tipo XML|xml|  
  
## <a name="see-also"></a>Consulte também  
[Referência da Interface de usuário &#40;DB2ToSQL&#41;](../../ssma/db2/user-interface-reference-db2tosql.md)  
  
