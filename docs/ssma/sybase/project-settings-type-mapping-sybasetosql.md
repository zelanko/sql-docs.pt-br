---
title: Configurações do projeto (mapeamento de tipo) (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2698fb3a-f9e6-4e04-94e0-dad289d7ed0a
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 148180d95bcbff1626069e72fb66dd9a3ca859c9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62667916"
---
# <a name="project-settings-type-mapping-sybasetosql"></a>Configurações do projeto (mapeamento de tipo) (SybaseToSQL)
A página de mapeamento de tipo de **configurações do projeto** caixa de diálogo contém configurações que personalizam como SSMA converte tipos de dados do Sybase Adaptive Server Enterprise (ASE) em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados.  
  
A página mapeamento de tipo está disponível na **configurações do projeto** e **configurações do projeto padrão** caixas de diálogo.  
  
-   Para especificar as configurações de mapeamento de tipo para todos os projetos futuros do SSMA, na **ferramentas** menu, selecione **configurações do projeto padrão**, selecione o tipo de projeto de migração para o qual as configurações são necessárias para ser exibido ou alterado de **versão de destino de migração** lista suspensa e, em seguida, selecione **mapeamento de tipo** na parte inferior do painel esquerdo.  
  
-   Para especificar configurações para o projeto atual, nos **ferramentas** menu, selecione **configurações do projeto**e, em seguida, selecione **mapeamento de tipo** na parte inferior do painel esquerdo.  
  
## <a name="options"></a>Opções  
**Tipo de Origem**  
O tipo de dados ASE mapeado.  
  
**Tipo de destino**  
O destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados para o tipo de dados especificado do ASE.  
  
Consulte a tabela na seção a seguir para o padrão do SSMA para Sybase mapeamento de tipo.  
  
**Adicionar**  
Clique para adicionar um tipo de dados à lista de mapeamento.  
  
**Editar**  
Clique para editar o tipo de dados selecionado na lista de mapeamento.  
  
**Remover**  
Clique para remover o mapeamento de tipo de dados selecionado da lista de mapeamento.  
  
**Restaurar Padrões**  
Clique para redefinir a lista de mapeamento de tipo para os padrões do SSMA.  
  
## <a name="default-type-mapping"></a>Mapeamento de tipo padrão  
A tabela a seguir contém o mapeamento de tipo padrão entre o ASE e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados.  
  
|Tipo de dados do ASE|Tipo de dados do SQL Server|  
|-----------------|------------------------|  
|**bigint**|**bigint**|  
|**binary**|**binary**|  
|**binary[\*..8000]**|**binary[\*]**|  
|**binary[8001..\*]**|**varbinary(max)**|  
|**bit**|**bit**|  
|**char**|**char**|  
|**char varying**|**varchar**|  
|**variando de char [\*... 8000]**|**varchar[\*]**|  
|**variando de char [8001...\*]**|**varchar(max)**|  
|**char[\*..8000]**|**char[\*]**|  
|**char[8001..\*;]**|**varchar(max)**|  
|**character**|**char**|  
|**a variável de caractere**|**varchar**|  
|**a variável de caractere [\*... 8000]**|**varchar[\*]**|  
|**a variável de caractere [8001...\*]**|**varchar(max)**|  
|**character[\*..8000]**|**char[\*]**|  
|**caracteres [8001...\*]**|**varchar(max)**|  
|**date**|**date**|  
|**datetime**|**datetime2[3]**|  
|**dec**|**decimal**|  
|**dec[\*..\*]**|**decimal[\*]**|  
|**dec[\*..\*][\*..\*]**|**decimal[\*][\*]**|  
|**decimal**|**decimal**|  
|**decimal[\*..\*]**|**decimal[\*]**|  
|**decimal[\*..\*][\*..\*]**|**decimal[\*][\*]**|  
|**precisão dupla**|**float[53]**|  
|**float**|**float[53]**|  
|**float[\*..15]**|**float[24]**|  
|**float [16...\*]**|**float[53]**|  
|**image**|**image**|  
|**int**|**int**|  
|**inteiro**|**int**|  
|**longsysname**|**nvarchar[255]**|  
|**money**|**money**|  
|**char nacional**|**nchar**|  
|**National char [\*... 4000]**|**nchar[\*]**|  
|**National char variados**|**nvarchar**|  
|**National char variados [\*... 4000]**|**nvarchar[\*]**|  
|**National char variados [4001...\*]**|**nvarchar(max)**|  
|**National char [4001...\*]**|**nvarchar(max)**|  
|**caracteres nacionais**|**nchar**|  
|**caractere nacional [\*... 4000]**|**nchar[\*]**|  
|**caractere nacional [4001...\*]**|**nvarchar(max)**|  
|**a variável de caracteres nacionais**|**nvarchar**|  
|**a variável de caractere nacional [\*... 4000]**|**nvarchar[\*]**|  
|**a variável de caractere nacional [4001...\*]**|**nvarchar(max)**|  
|**national varchar**|**nvarchar**|  
|**national varchar[\*..4000]**|**nvarchar[\*]**|  
|**varchar nacional [4001...\*]**|**nvarchar(max)**|  
|**nchar**|**nchar**|  
|**nchar varying**|**nvarchar**|  
|**nchar variados [\*... 4000]**|**nvarchar[\*]**|  
|**nchar variados [4001...\*]**|**nvarchar(max)**|  
|**nchar[\*..4000]**|**nchar[\*]**|  
|**nchar[4001..\*]**|**nvarchar(max)**|  
|**numeric**|**numeric**|  
|**numeric[\*..\*]**|**numeric[\*]**|  
|**numeric[\*..\*][\*..\*]**|**numeric[\*][\*]**|  
|**nvarchar**|**nvarchar**|  
|**nvarchar[\*..4000]**|**nvarchar[\*]**|  
|**nvarchar[4001..\*]**|**nvarchar(max)**|  
|**real**|**float[24]**|  
|**smalldatetime**|**smalldatetime**|  
|**smallint**|**smallint**|  
|**smallmoney**|**smallmoney**|  
|**sysname**|**nvarchar[128]**|  
|**sysname[\*..\*]**|**nvarchar[255]**|  
|**text**|**text**|  
|**time**|**time[3]**|  
|**timestamp**|**rowversion**|  
|**tinyint**|**tinyint**|  
|**unichar**|**nchar**|  
|**unichar varying**|**nvarchar**|  
|**variando UNICHAR [\*... 4000]**|**nvarchar[\*]**|  
|**variando UNICHAR [4001...\*]**|**nvarchar(max)**|  
|**unichar[\*..4000]**|**nchar[\*]**|  
|**unichar[4001..\*]**|**nvarchar(max)**|  
|**unitext**|**nvarchar(max)**|  
|**univarchar**|**nvarchar**|  
|**univarchar[\*..4000]**|**nvarchar[\*]**|  
|**univarchar[4001..\*]**|**nvarchar(max)**|  
|**unsigned bigint**|**numeric[20][0]**|  
|**unsigned int**|**bigint**|  
|**unsigned smallint**|**int**|  
|**tinyint sem sinal**|**tinyint**|  
|**varbinary**|**varbinary**|  
|**varbinary[\*..8000]**|**varbinary[\*]**|  
|**varbinary[8001..\*]**|**varbinary(max)**|  
|**varchar**|**varchar**|  
|**varchar[\*..8000]**|**varchar[\*]**|  
|**varchar[8001..\*]**|**varchar(max)**|  
  
