---
title: Gerar e executar o script de log suplementar | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- supLog
ms.assetid: 6e940d93-12c6-4cda-9333-5489b245f0e4
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: dcfeca9b451f0238a7148cbb9f1f60d4719ebe3a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48169906"
---
# <a name="generate-and-run-the-supplemental-logging-script"></a>Gerar e executar scripts de log suplementares
  Use a página Configurar tabelas para capturar alterações para executar um script no banco de dados de origem Oracle que configura o registro em log suplementar.  
  
 **Para executar os scripts suplementares de registro em log**  
  
 Clique em **Executar Script** para executar o script suplementar de registro em log nas tabelas definidas para a instância CDC. Este script instrui o banco de dados Oracle para gravar todas as colunas de interesse em seus logs de transação ao registrar em log operações UPDATE para tabelas capturadas. Este script é examinado e executado normalmente por um administrador do sistema Oracle.  
  
 Você também pode executar os scripts manualmente usando o SQL * Plus.  
  
 **Para executar os scripts manualmente**  
  
 Clique em **Copiar** para colar o script na área de transferência. Abra o SQL * Plus e vá para o diretório com seu banco de dados de origem Oracle. Cole o script no SQL\*Plus para executar isto.  
  
 Para salvar o script de log suplementar em um arquivo de texto, clique em **Salvar como** e navegue até o local onde você deseja salvar o arquivo. Dê ao arquivo um nome e clique em **Salvar** para salvar o arquivo.  
  
 Clique em **Avançar** para [Generate Mirror Tables and CDC Capture Instances](generate-mirror-tables-and-cdc-capture-instances.md).  
  
## <a name="see-also"></a>Consulte também  
 [Como criar a instância de banco de dados de alteração do SQL Server](how-to-create-the-sql-server-change-database-instance.md)   
 [Examinar e gerar scripts de log suplementares](review-and-generate-supplemental-logging-scripts.md)  
  
  
