---
title: "Configurações (mapeamento de tipo) do projeto (SybaseToSQL) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 2698fb3a-f9e6-4e04-94e0-dad289d7ed0a
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 77c02b875a22fefec54c59518f4972cbd7aefd4b
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="project-settings-type-mapping-sybasetosql"></a>Configurações (mapeamento de tipo) do projeto (SybaseToSQL)
A página mapeamento de tipo do **configurações de projeto** caixa de diálogo contém configurações que personalizam como o SSMA converte tipos de dados do Sybase Adaptive Server Enterprise (ASE) em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de dados.  
  
A mapeamento de tipo de página está disponível na **configurações de projeto** e **configurações de projeto padrão** caixas de diálogo.  
  
-   Para especificar as configurações de mapeamento de tipo para todos os projetos futuros do SSMA, no **ferramentas** menu, selecione **configurações de projeto padrão**, selecione o tipo de projeto de migração para o qual as configurações são necessárias para ser exibido ou alterado de **versão de destino de migração** lista suspensa e, em seguida, selecione **mapeamento de tipo** na parte inferior do painel esquerdo.  
  
-   Para especificar as configurações para o projeto atual, no **ferramentas** menu, selecione **configurações de projeto**e, em seguida, selecione **mapeamento de tipo** na parte inferior do painel esquerdo.  
  
## <a name="options"></a>Opções  
**Tipo de Origem**  
O tipo de dados ASE mapeado.  
  
**Tipo de destino**  
O destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipo de dados para o tipo de dados ASE especificado.  
  
Consulte a tabela na seção a seguir para o padrão do SSMA para Sybase mapeamento de tipo.  
  
**Adicionar**  
Clique para adicionar um tipo de dados para a lista de mapeamento.  
  
**Editar**  
Clique para editar o tipo de dados selecionado na lista de mapeamento.  
  
**Remover**  
Clique para remover o mapeamento de tipo de dados selecionado da lista de mapeamento.  
  
**Redefinir para padrão**  
Clique para redefinir a lista de mapeamento de tipo para os padrões do SSMA.  
  
## <a name="default-type-mapping"></a>Mapeamento de tipo padrão  
A tabela a seguir contém o mapeamento de tipo padrão entre ASE e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de dados.  
  
|Tipo de dados ASE|Tipo de dados do SQL Server|  
|-----------------|------------------------|  
|**bigint**|**bigint**|  
|**binary**|**binary**|  
|**binário [\*...8000]**|**binário [\*]**|  
|**binário [8001...\*]**|**varbinary(max)**|  
|**bit**|**bit**|  
|**char**|**char**|  
|**char variados**|**varchar**|  
|**variável de char [\*...8000]**|**varchar [\*]**|  
|**variável de char [8001...\*]**|**varchar(max)**|  
|**char[\*..8000]**|**char[\*]**|  
|**char [8001...\& #42;]**|**varchar(max)**|  
|**caractere**|**char**|  
|**variável de caractere**|**varchar**|  
|**variável de caractere [\*...8000]**|**varchar [\*]**|  
|**variável de caractere [8001...\*]**|**varchar(max)**|  
|**caracteres [\*...8000]**|**char[\*]**|  
|**caracteres [8001...\*]**|**varchar(max)**|  
|**date**|**date**|  
|**datetime**|**datetime2 [3]**|  
|**DEC**|**decimal**|  
|**dec[\*..\*]**|**decimal [\*]**|  
|**dec[\*..\*][\*..\*]**|**decimal[\*][\*]**|  
|**decimal**|**decimal**|  
|**decimal [\*...\*]**|**decimal [\*]**|  
|**decimal [\*...\*][\*..\*]**|**decimal[\*][\*]**|  
|**precisão dupla**|**float [53]**|  
|**float**|**float [53]**|  
|**float [\*...15]**|**float [24]**|  
|**float [16 …\*]**|**float [53]**|  
|**image**|**image**|  
|**Int**|**Int**|  
|**inteiro**|**Int**|  
|**longsysname**|**nvarchar [255]**|  
|**money**|**money**|  
|**National char**|**nchar**|  
|**National char [\*...4000]**|**nchar [\*]**|  
|**variável de caractere nacional**|**nvarchar**|  
|**variável de caractere nacional [\*...4000]**|**nvarchar [\*]**|  
|**variável de caractere nacional [4001.\*]**|**nvarchar(max)**|  
|**National char [4001.\*]**|**nvarchar(max)**|  
|**caracteres nacionais**|**nchar**|  
|**caracteres nacionais [\*...4000]**|**nchar [\*]**|  
|**caracteres nacionais [4001.\*]**|**nvarchar(max)**|  
|**variável de caracteres nacionais**|**nvarchar**|  
|**variável de caractere nacional [\*...4000]**|**nvarchar [\*]**|  
|**variável de caractere nacional [4001.\*]**|**nvarchar(max)**|  
|**varchar nacional**|**nvarchar**|  
|**National varchar [\*...4000]**|**nvarchar [\*]**|  
|**National varchar [4001.\*]**|**nvarchar(max)**|  
|**nchar**|**nchar**|  
|**nchar variados**|**nvarchar**|  
|**nchar variados [\*...4000]**|**nvarchar [\*]**|  
|**nchar variados [4001.\*]**|**nvarchar(max)**|  
|**nchar [\*...4000]**|**nchar [\*]**|  
|**nchar [4001.\*]**|**nvarchar(max)**|  
|**numeric**|**numeric**|  
|**numérico [\*...\*]**|**numérico [\*]**|  
|**numérico [\*...\*][\*..\*]**|**numeric[\*][\*]**|  
|**nvarchar**|**nvarchar**|  
|**nvarchar [\*...4000]**|**nvarchar [\*]**|  
|**nvarchar [4001.\*]**|**nvarchar(max)**|  
|**real**|**float [24]**|  
|**smalldatetime**|**smalldatetime**|  
|**smallint**|**smallint**|  
|**smallmoney**|**smallmoney**|  
|**sysname**|**nvarchar [128]**|  
|**sysname [\*...\*]**|**nvarchar [255]**|  
|**text**|**text**|  
|**time**|**tempo [3]**|  
|**timestamp**|**rowversion**|  
|**tinyint**|**tinyint**|  
|**UNICHAR**|**nchar**|  
|**UNICHAR variados**|**nvarchar**|  
|**variável UNICHAR [\*...4000]**|**nvarchar [\*]**|  
|**variável UNICHAR [4001.\*]**|**nvarchar(max)**|  
|**UNICHAR [\*...4000]**|**nchar [\*]**|  
|**UNICHAR [4001.\*]**|**nvarchar(max)**|  
|**unitext**|**nvarchar(max)**|  
|**univarchar**|**nvarchar**|  
|**univarchar [\*...4000]**|**nvarchar [\*]**|  
|**univarchar [4001.\*]**|**nvarchar(max)**|  
|**bigint não assinado**|**numérico [20] [0]**|  
|**int não assinado**|**bigint**|  
|**smallint não assinado**|**Int**|  
|**tinyint não assinado**|**tinyint**|  
|**varbinary**|**varbinary**|  
|**varbinary [\*...8000]**|**varbinary [\*]**|  
|**varbinary [8001...\*]**|**varbinary(max)**|  
|**varchar**|**varchar**|  
|**varchar [\*...8000]**|**varchar [\*]**|  
|**varchar [8001...\*]**|**varchar(max)**|  
  

