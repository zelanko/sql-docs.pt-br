---
title: SQL Server Management Studio – Telemetria (SSMS) | Microsoft Docs
ms.custom: ''
ms.date: 02/20/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c28ffa44-7b8b-4efa-b755-c7a3b1c11ce4
caps.latest.revision: 72
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f11f205a4a0baf5db2344ed7b365b0bc2fde4dd9
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="local-audit-for-ssms-usage-feedback-collection"></a>Auditoria local da coleta de comentários sobre o uso do SSMS
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
O SSMS (SQL Server Management Studio) contém recursos habilitados para Internet que podem coletar e enviar os dados anônimos de uso de recursos à Microsoft. O SSMS pode coletar informações padrão do computador e informações de uso e desempenho que podem ser transmitidas à Microsoft e analisadas com a finalidade de aprimorar a qualidade, a segurança e a confiabilidade do SSMS. Não coletamos dados como o seu nome, endereço ou outras informações de contato. Para obter detalhes, consulte a [Política de Privacidade do SQL Server](https://www.microsoft.com/en-us/privacystatement/SQLServer/Default.aspx).

## <a name="audit-feature-usage-data"></a>Dados de uso do recurso de auditoria

Para ver os dados de uso do recurso que são coletados pelo SSMS, faça o seguinte:
1.  Inicie o SSMS.
2.  Clique em **Exibir**, depois clique em **Saída** no menu principal para mostrar a janela **Saída**. 
3.  Quando a janela **Saída** estiver visível, escolha **Telemetria** no menu **Mostrar saída de:**.

Ao usar o SSMS para interagir com bancos de dados, a janela **Saída** mostra os dados coletados.

## <a name="enable-or-disable-usage-feedback-collection-in-ssms"></a>Habilitar ou desabilitar a coleta de comentários sobre o uso no SSMS

Para optar por realizar ou não a coleta de dados de uso para SSMS, consulte: [Como configurar o SQL Server 2016 para enviar comentários à Microsoft](http://support.microsoft.com/help/3153756/how-to-configure-sql-server-2016-to-send-feedback-to-microsoft).

## <a name="see-also"></a>Confira também

[Auditoria Local da coleta de comentários sobre o uso do SQL Server](http://msdn.microsoft.com/library/mt743085.aspx)
