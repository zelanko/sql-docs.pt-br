---
description: Conectar-se ao Oracle
title: Conecte-se ao Oracle | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- connOra
ms.assetid: 711ac7ff-5d3d-4533-80ca-d1fecdb3048f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c628f77c74c16bd196a496e7cacf27a0f2904e12
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88496229"
---
# <a name="connect-to-oracle"></a>Conectar-se ao Oracle

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Quando você adiciona ou edita as tabelas usadas na instância de CDC pela primeira vez, você deverá se conectar ao banco de dados Oracle. Você deve inserir as credenciais de um usuário Oracle que pode acessar o esquema das tabelas a ser capturado. Insira o seguinte nesta caixa de diálogo:  
  
 **Autenticação**  
  
 Selecione uma das seguintes:  
  
-   **Autenticação do Windows**: selecione isto para usar as credenciais de domínio atuais do Windows. Você só poderá usar esta opção se o banco de dados Oracle estiver configurado para funcionar com autenticação do Windows.  
  
-   **Autenticação do Oracle**: se você selecionou esta opção, deve digitar o **Nome de usuário** e **Senha** para o usuário no banco de dados Oracle ao qual você está se conectando.  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar tabelas a uma instância CDC](../../integration-services/change-data-capture/add-tables-to-a-cdc-instance.md)  
  
  
