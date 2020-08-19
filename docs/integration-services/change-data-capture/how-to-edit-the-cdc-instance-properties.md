---
description: Como editar as propriedades de instância CDC
title: Como editar as propriedades de instância CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7a6c719a-3735-43b7-b3ab-dfadd325eca2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ee2861b40dbe132e7c95b52802bd10ccd46c20c1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88426088"
---
# <a name="how-to-edit-the-cdc-instance-properties"></a>Como editar as propriedades de instância CDC

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Este procedimento descreve como usar o CDC Designer Console para editar as propriedades de configuração para uma instância CDC.  
  
### <a name="to-edit-the-cdc-instance-configuration-properties"></a>Para editar as propriedades de configuração da instância CDC  
  
1.  No menu **Iniciar** , selecione o **CDC Designer Console**.  
  
2.  No painel esquerdo, expanda **Change Data Capture** e, em seguida, expanda o serviço que contém a instância com as propriedades que você quer editar.  
  
3.  Selecione o nome da instância onde você quer editar as propriedades.  
  
4.  No painel Actions no lado direito do CDC Designer Console, clique em **Properties**.  
  
     Você também pode clicar com o botão direito do mouse na instância em que deseja editar as propriedades e clique em **Properties**.  
  
5.  No editor de Properties, edite as propriedades nas guias a seguir:  
  
    -   **Oracle**: use a guia **Oracle** no editor de Propriedades para fazer alterações na descrição fornecida na página Create CDC database no assistente de Nova Instância e fazer alterações nas informações de conexão de banco de dados de mineração de logs do Oracle.  
  
         Para obter mais informações sobre o que você pode editar nessa guia, consulte [Edit the Oracle Database Properties](../../integration-services/change-data-capture/edit-the-oracle-database-properties.md).  
  
    -   **Tables**: use a guia **Tables** para fazer alterações às tabelas e colunas selecionadas do banco de dados de origem Oracle.  
  
         Para obter mais informações sobre o que você pode editar nessa guia, consulte Edit [Edit Tables](../../integration-services/change-data-capture/edit-tables.md).  
  
    -   **Scripts**: use a guia **Scripts** para executar ou executar novamente um script no banco de dados de origem Oracle que configura o registro em log suplementar.  
  
         Para obter mais informações sobre o que você pode fazer nessa guia, consulte [Review and Generate Supplemental Logging Scripts](../../integration-services/change-data-capture/review-and-generate-supplemental-logging-scripts.md).  
  
    -   **Advanced**: use a guia **Advanced** para acrescentar propriedades especiais à instância de CDC.  
  
         Para obter mais informações sobre o que você pode fazer nessa guia, consulte [Edit the Advanced Properties](../../integration-services/change-data-capture/edit-the-advanced-properties.md).  
  
  
