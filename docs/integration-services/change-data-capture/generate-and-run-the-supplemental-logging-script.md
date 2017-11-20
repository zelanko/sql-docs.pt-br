---
title: Gerar e executar o Script de registro em log suplementar | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: change-data-capture
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- supLog
ms.assetid: 6e940d93-12c6-4cda-9333-5489b245f0e4
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 736b11e79235b38659e9fa4c13f06369bd8b335d
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="generate-and-run-the-supplemental-logging-script"></a>Gerar e executar scripts de log suplementares
  Use a página Configurar tabelas para capturar alterações para executar um script no banco de dados de origem Oracle que configura o registro em log suplementar.  
  
 **Para executar os scripts suplementares de registro em log**  
  
 Clique em **Executar Script** para executar o script suplementar de registro em log nas tabelas definidas para a instância CDC. Este script instrui o banco de dados Oracle para gravar todas as colunas de interesse em seus logs de transação ao registrar em log operações UPDATE para tabelas capturadas. Este script é examinado e executado normalmente por um administrador do sistema Oracle.  
  
 Você também pode executar os scripts manualmente usando o SQL * Plus.  
  
 **Para executar os scripts manualmente**  
  
 Clique em **Copiar** para colar o script na área de transferência. Abra o SQL * Plus e vá para o diretório com seu banco de dados de origem Oracle. Cole o script no SQL\*Plus para executar isto.  
  
 Para salvar o script de log suplementar em um arquivo de texto, clique em **Salvar como** e navegue até o local onde você deseja salvar o arquivo. Dê ao arquivo um nome e clique em **Salvar** para salvar o arquivo.  
  
 Clique em **Avançar** para [Generate Mirror Tables and CDC Capture Instances](../../integration-services/change-data-capture/generate-mirror-tables-and-cdc-capture-instances.md).  
  
## <a name="see-also"></a>Consulte também  
 [Como criar a instância de banco de dados de alteração do SQL Server](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [Revisar e gerar Scripts de log suplementares](../../integration-services/change-data-capture/review-and-generate-supplemental-logging-scripts.md)  
  
  

