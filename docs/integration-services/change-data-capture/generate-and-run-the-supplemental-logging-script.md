---
title: Gerar e executar o script de log suplementar | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- supLog
ms.assetid: 6e940d93-12c6-4cda-9333-5489b245f0e4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 91f76644545af1c53ac72d293907da7fb2be17f4
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58273855"
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
  
## <a name="see-also"></a>Consulte Também  
 [Como criar a instância de banco de dados de alteração do SQL Server](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [Revisar e gerar scripts de log suplementares](../../integration-services/change-data-capture/review-and-generate-supplemental-logging-scripts.md)  
  
  
