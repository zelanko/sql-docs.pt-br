---
title: Migrar logons SQL Server com Assistente de Migração de Dados
description: Saiba como migrar logons do SQL Server com Assistente de Migração de Dados
ms.date: 10/22/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, login migration
ms.assetid: ''
author: rajeshsetlem
ms.author: rajpo
ms.custom: seo-lt-2019
ms.openlocfilehash: f721800de13d11eefa1cabdd2f23fda838db9396
ms.sourcegitcommit: fb1430aedbb91b55b92f07934e9b9bdfbbd2b0c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82885783"
---
# <a name="migrate-sql-server-logins-with-data-migration-assistant"></a>Migrar logons SQL Server com Assistente de Migração de Dados

Este artigo fornece uma visão geral da migração de logons SQL Server usando o Assistente de Migração de Dados.

> [!IMPORTANT]
> Este tópico se aplica a cenários que envolvem atualizações de SQL Server para versões posteriores do produto local ou para SQL Server em máquinas virtuais do Azure.

## <a name="which-logins-are-migrated"></a>Quais logons são migrados

- Você pode migrar os logons com base em uma entidade de segurança do Windows (como um usuário de domínio ou um grupo de domínio do Windows). Você também pode migrar logons criados com base na autenticação do SQL, também chamados de logons do SQL Server.

- Atualmente, Assistente de Migração de Dados não dá suporte aos logons associados a um certificado de segurança autônomo (logons mapeados para o certificado), uma chave assimétrica autônoma (logons mapeados para a chave assimétrica) e logons mapeados para credenciais.

- Assistente de Migração de Dados não move o logon **SA** e os princípios de servidor com nomes entre marcas de hash duplos ( \# \# ), que são apenas para uso interno.

- Por padrão, Assistente de Migração de Dados seleciona todos os logons qualificados para migrar. Opcionalmente, você pode selecionar logons específicos para migrar. Quando Assistente de Migração de Dados migra todos os logons qualificados, o mapeamento de usuário de logon permanece intacto nos bancos de dados que são migrados.

  Se você planeja migrar logons específicos, certifique-se de selecionar os logons que são mapeados para um ou mais usuários nos bancos de dados selecionados para migração.

- Como parte da migração de logon, Assistente de Migração de Dados também move funções de servidor definidas pelo usuário e adiciona permissões de nível de servidor às funções de servidor definidas pelo usuário. O proprietário da função será definido como entidade **SA** .

## <a name="during-and-after-migration"></a>Durante e após a migração

- Como parte da migração de logon, Assistente de Migração de Dados atribui as permissões aos protegíveis no SQL Server de destino como existem no SQL Server de origem.

  Se o logon já existir no SQL Server de destino, Assistente de Migração de Dados migrará apenas as permissões atribuídas a protegíveis e não criará novamente o logon inteiro.

- Assistente de Migração de Dados torna o melhor esforço para mapear o logon para usuários de banco de dados se o logon já existir no servidor de destino.

- É recomendável que você revise os resultados da migração para entender o status geral da migração de logon e as ações de pós-atualização recomendadas.

## <a name="resources"></a>Recursos

[AMD (Assistente de Migração de Dados)](../dma/dma-overview.md)

[Assistente de Migração de Dados: definições de configuração](../dma/dma-configurationsettings.md)
