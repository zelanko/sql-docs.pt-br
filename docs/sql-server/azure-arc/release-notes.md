---
title: SQL Server habilitado para Azure Arc – Notas sobre a versão
description: Notas sobre a versão mais recentes
author: anosov1960
ms.author: sashan
ms.reviewer: mikeray
ms.date: 10/29/2020
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 3dcbc6b17d5abe87aabe923d70746d65595b9de6
ms.sourcegitcommit: dc3ea1696b8a4332934568439aed6cce4e9737eb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93244648"
---
# <a name="release-notes---azure-arc-enabled-sql-server-preview"></a>Notas sobre a versão – SQL Server habilitado para Azure Arc (versão prévia)

> [!NOTE]
> Como uma versão prévia do recurso, a tecnologia apresentada neste artigo está sujeita aos [Termos de uso complementares para versões prévias do Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## <a name="september-2020"></a>Setembro de 2020

O SQL Server habilitado para Azure Arc foi lançado na versão prévia pública. O SQL Server habilitado para Azure Arc estende os serviços do Azure para instâncias do SQL Server hospedadas fora do Azure no datacenter do cliente, na borda ou em um ambiente de várias nuvens.

Para conhecer os detalhes, confira [Visão geral do SQL Server habilitado para Azure Arc](overview.md)

### <a name="known-issues"></a>Problemas conhecidos

Os seguintes problemas se aplicam à versão de setembro:

* A folha **Registrar o SQL Server habilitado para Azure Arc** não dá suporte à configuração de marcas personalizadas. Para adicionar marcas personalizadas, abra o recurso **SQL Server – Azure Arc** após o registro e altere as Marcas na página **Visão geral**.

* Conectar instâncias do SQL Server ao Azure Arc requer uma conta com um conjunto amplo de permissões. Para conhecer os detalhes, confira [Permissões necessárias](overview.md#required-permissions).

## <a name="october-2020"></a>Outubro de 2020

A atualização de outubro inclui os seguintes aprimoramentos:

* Agora, a folha Registrar SQL Server habilitado para Azure Arc inclui a guia **Marcas**. As marcas são incluídas no script de registro e são refletidas no recurso **SQL Server – Azure Arc**. Para conhecer os detalhes, confira [Conectar o SQL Server ao Azure Arc](connect.md).

* Agora, a entrada **Integridade do Ambiente** dá suporte à ativação da **Avaliação do SQL** no Portal implantando uma *CustomScriptExtension*. Para conhecer os detalhes, confira [Configurar a Avaliação do SQL](assess.md#run-on-demand-sql-assessment).

### <a name="known-issues"></a>Problemas conhecidos

Os seguintes problemas se aplicam à versão de outubro:

* Conectar instâncias do SQL Server ao Azure Arc requer uma conta com um conjunto amplo de permissões. Para conhecer os detalhes, confira [Permissões necessárias](overview.md#required-permissions).

## <a name="next-steps"></a>Próximas etapas

**Quer apenas experimentar as novidades?**  Comece rapidamente em [Início rápido do SQL Server habilitado para Azure Arc](https://aka.ms/AzureArcSqlServerJumpstart).
