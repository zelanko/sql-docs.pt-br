---
description: Configurações do projeto (mapeamento de tipo) (SybaseToSQL)
title: Configurações do projeto (mapeamento de tipo) (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2698fb3a-f9e6-4e04-94e0-dad289d7ed0a
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 99ab880b69d2c06d462ed42ca0a2529ba6bf7bc2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88372112"
---
# <a name="project-settings-type-mapping-sybasetosql"></a>Configurações do projeto (mapeamento de tipo) (SybaseToSQL)
A página mapeamento de tipos da caixa de diálogo **configurações do projeto** contém configurações que personalizam como o SSMA converte os tipos de dados do ase Adaptive Server Enterprise para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] os tipos de dados.  
  
A página mapeamento de tipo está disponível nas caixas de diálogo **configurações do projeto** e **configurações do projeto padrão** .  
  
-   Para especificar as configurações de mapeamento de tipo para todos os projetos do SSMA futuros, no menu **ferramentas** , selecione **configurações de projeto padrão**, selecione tipo de projeto de migração para o qual as configurações devem ser exibidas ou alteradas no menu suspenso **versão de destino de migração** e selecione mapeamento de **tipo** na parte inferior do painel esquerdo.  
  
-   Para especificar as configurações do projeto atual, no menu **ferramentas** , selecione **configurações do projeto**e, em seguida, selecione **mapeamento de tipo** na parte inferior do painel esquerdo.  
  
## <a name="options"></a>Opções  
**Tipo de origem**  
O tipo de dados do ASE mapeado.  
  
**Tipo de destino**  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados de destino para o tipo de dados do ase especificado.  
  
Consulte a tabela na seção a seguir para o mapeamento de tipo do SSMA para Sybase padrão.  
  
**Adicionar**  
Clique para adicionar um tipo de dados à lista de mapeamento.  
  
**Editar**  
Clique para editar o tipo de dados selecionado na lista mapeamento.  
  
**Remover**  
Clique para remover o mapeamento de tipo de dados selecionado da lista de mapeamento.  
  
**Restaurar Padrões**  
Clique para redefinir a lista de mapeamento de tipo para os padrões do SSMA.  
  
## <a name="default-type-mapping"></a>Mapeamento de tipo padrão  
A tabela a seguir contém o mapeamento de tipo padrão entre o ASE e os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados.  
  
|Tipo de dados do ASE|Tipo de dados do SQL Server|  
|-----------------|------------------------|  
|**bigint**|**bigint**|  
|**binary**|**binary**|  
|**binário [ \* .. 8000]**|**binário [ \* ]**|  
|**binário [8001.. \* ]**|**varbinary(max)**|  
|**bit**|**bit**|  
|**char**|**char**|  
|**char varying**|**varchar**|  
|**variável de caractere [ \* .. 8000]**|**varchar [ \* ]**|  
|**variação de caractere [8001.. \* ]**|**varchar(max)**|  
|**Char [ \* .. 8000]**|**Char [ \* ]**|  
|**Char [8001.. \* ;]**|**varchar(max)**|  
|**espaço**|**char**|  
|**character varying**|**varchar**|  
|**variável de caractere [ \* .. 8000]**|**varchar [ \* ]**|  
|**variável de caractere [8001.. \* ]**|**varchar(max)**|  
|**caractere [ \* .. 8000]**|**Char [ \* ]**|  
|**caractere [8001.. \* ]**|**varchar(max)**|  
|**date**|**date**|  
|**datetime**|**datetime2 [3]**|  
|**dez**|**decimal**|  
|**Dec [ \* .. \* ]**|**Decimal [ \* ]**|  
|**Dec [ \* .. \* ] [\*..\*]**|**Decimal [ \* ] [ \* ]**|  
|**decimal**|**decimal**|  
|**Decimal [ \* .. \* ]**|**Decimal [ \* ]**|  
|**Decimal [ \* .. \* ] [\*..\*]**|**Decimal [ \* ] [ \* ]**|  
|**precisão dupla**|**float [53]**|  
|**float**|**float [53]**|  
|**float [ \* .. 15**|**float [24]**|  
|**float [16.. \* ]**|**float [53]**|  
|**imagem**|**imagem**|  
|**int**|**int**|  
|**inteiro**|**int**|  
|**longsysname**|**nvarchar [255]**|  
|**money**|**money**|  
|**caractere nacional**|**nchar**|  
|**caractere nacional [ \* .. 4000]**|**nchar [ \* ]**|  
|**variação de caractere nacional**|**nvarchar**|  
|**variação de caractere nacional [ \* .. 4000]**|**nvarchar [ \* ]**|  
|**variação de caractere nacional [4001.. \* ]**|**nvarchar(max)**|  
|**caractere nacional [4001.. \* ]**|**nvarchar(max)**|  
|**caractere nacional**|**nchar**|  
|**caractere nacional [ \* .. 4000]**|**nchar [ \* ]**|  
|**caractere nacional [4001.. \* ]**|**nvarchar(max)**|  
|**variação de caractere nacional**|**nvarchar**|  
|**variação de caractere nacional [ \* .. 4000]**|**nvarchar [ \* ]**|  
|**variação de caractere nacional [4001.. \* ]**|**nvarchar(max)**|  
|**varchar nacional**|**nvarchar**|  
|**varchar [ \* .. 4000]**|**nvarchar [ \* ]**|  
|**varchar [4001.. \* ] nacional**|**nvarchar(max)**|  
|**nchar**|**nchar**|  
|**variável nchar**|**nvarchar**|  
|**nchar variando [ \* .. 4000]**|**nvarchar [ \* ]**|  
|**nchar variável [4001.. \* ]**|**nvarchar(max)**|  
|**nchar [ \* .. 4000]**|**nchar [ \* ]**|  
|**nchar [4001.. \* ]**|**nvarchar(max)**|  
|**numeric**|**numeric**|  
|**numérico [ \* .. \* ]**|**numeric [ \* ]**|  
|**numérico [ \* .. \* ] [\*..\*]**|**numeric [ \* ] [ \* ]**|  
|**nvarchar**|**nvarchar**|  
|**nvarchar [ \* .. 4000]**|**nvarchar [ \* ]**|  
|**nvarchar [4001.. \* ]**|**nvarchar(max)**|  
|**real**|**float [24]**|  
|**smalldatetime**|**smalldatetime**|  
|**smallint**|**smallint**|  
|**smallmoney**|**smallmoney**|  
|**sysname**|**nvarchar [128]**|  
|**sysname [ \* .. \* ]**|**nvarchar [255]**|  
|**text**|**text**|  
|**time**|**hora [3]**|  
|**timestamp**|**rowversion**|  
|**tinyint**|**tinyint**|  
|**unichar**|**nchar**|  
|**variável UNICHAR**|**nvarchar**|  
|**UNICHAR variando [ \* .. 4000]**|**nvarchar [ \* ]**|  
|**variável UNICHAR [4001.. \* ]**|**nvarchar(max)**|  
|**UNICHAR [ \* .. 4000]**|**nchar [ \* ]**|  
|**UNICHAR [4001.. \* ]**|**nvarchar(max)**|  
|**unitext**|**nvarchar(max)**|  
|**univarchar**|**nvarchar**|  
|**univarchar [ \* .. 4000]**|**nvarchar [ \* ]**|  
|**univarchar [4001.. \* ]**|**nvarchar(max)**|  
|**bigint não assinado**|**numeric [20] [0]**|  
|**unsigned int**|**bigint**|  
|**smallint não assinado**|**int**|  
|**tinyint não assinado**|**tinyint**|  
|**varbinary**|**varbinary**|  
|**varbinary [ \* .. 8000]**|**varbinary [ \* ]**|  
|**varbinary [8001.. \* ]**|**varbinary(max)**|  
|**varchar**|**varchar**|  
|**varchar [ \* .. 8000]**|**varchar [ \* ]**|  
|**varchar [8001.. \* ]**|**varchar(max)**|  
  
