---
title: Migrando os logons do SQL Server (Assistente de migração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 08/31/2017
ms.prod: sql
ms.prod_service: dma
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-dma
ms.tgt_pltfrm: ''
ms.topic: article
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, login migration
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 45836159a2708166dc367c73a03f33d75eabe850
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="migrating-sql-server-logins-using-data-migration-assistant"></a>Migrando logons do SQL Server usando o Assistente de migração de dados

Este artigo fornece uma visão geral da migração logons do SQL Server usando o Assistente de migração de dados. 

## <a name="key-concepts"></a>Conceitos principais
Estes são os principais conceitos.

- Você pode migrar os logons com base em uma entidade de segurança do Windows (como um usuário de domínio ou um grupo de domínio do Windows). Também é possível migrar os logons criados com base na autenticação do SQL, também chamada de logons do SQL Server.

- Assistente de migração de dados atualmente não dá suporte os logons associados com um certificado de segurança autônomo (logons mapeados para certificados), uma chave assimétrica autônoma (logons mapeados para chave assimétrica) e logons mapeados para as credenciais.

- Assistente de migração de dados não move o **sa** princípios de logon e o servidor com nomes entre duas marcas hash (\#\#), que são somente para uso interno.

- Por padrão, Assistatn de migração de dados seleciona todos os logons qualificados para migração. Opcionalmente, você pode selecionar os logons específicos para migrar. Quando o Assistente de migração de dados migra todos os logons qualificados, o mapeamento de usuário do logon permanece intacto em bancos de dados que são migrados. 

  Se você planeja migrar logons específicos, certifique-se de selecionar os logons que são mapeados para um ou mais usuários nos bancos de dados selecionados para migração.

- Como parte da migração de logon, Assistente de migração de dados também move as funções de servidor definidas pelo usuário e adiciona permissões em nível de servidor para as funções de servidor definidas pelo usuário. O proprietário da função será definido como **sa** principal.

- Como parte da migração de logon, o Assistente de migração de dados atribui as permissões para protegíveis no SQL Server de destino que existem no SQL Server de origem. 

  Se o logon já existe no destino do SQL Server, o Assistente de migração de dados migra apenas as permissões atribuídas a protegíveis e não recriará o logon de todo.

- Assistente de migração de dados torna-se melhor esforço para mapear o logon para os usuários de banco de dados se o logon já existe no servidor de destino.

- É recomendável que você revise os resultados de migração para entender o status geral de todas as ações recomendadas após a migração e a migração de logon.

## <a name="resources"></a>Recursos

[Assistente de migração de dados (DMA)](../dma/dma-overview.md)

[Assistente de migração de dados: Definições de configuração](../dma/dma-configurationsettings.md)
