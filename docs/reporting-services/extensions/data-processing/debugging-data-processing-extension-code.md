---
title: "Depurando código de extensão de processamento de dados | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- debugging data processing extensions [Reporting Services]
- troubleshooting [Reporting Services], data processing extensions
- data processing extensions [Reporting Services], debugging
ms.assetid: e963e205-9ae0-446d-97df-028a1d2727d9
caps.latest.revision: 40
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 0b7ee42be2f3d54fc8fb19ab48b3b603e29669e2
ms.contentlocale: pt-br
ms.lasthandoff: 08/12/2017

---
# <a name="debugging-data-processing-extension-code"></a>Depurando o código de extensão de processamento de dados
  O [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] fornece várias ferramentas de depuração que podem ajudá-lo a analisar seu código de extensão de processamento de dados e localizar erros nele. A ferramenta mais adequada dependerá do que você está tentando realizar. Este exemplo usa o [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)].  
  
#### <a name="to-debug-your-data-processing-extension-code"></a>Para depurar seu código de extensão de processamento de dados  
  
1.  Inicie o [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)] e abra seu projeto de extensão de processamento de dados.  
  
2.  Crie o projeto e implante seu assembly de extensão de processamento de dados e o arquivo .pdb anexo ao Designer de Relatórios. Para obter mais informações sobre a implantação, consulte [como: implantar uma extensão de processamento de dados no Designer de relatórios](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension-to-report-designer.md).  
  
3.  Abra um novo Projeto de Relatório no [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] enquanto deixa seu código de extensão de processamento de dados aberto em uma janela separada do [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
4.  Navegue até a janela do [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] que contém seu projeto de extensão de processamento de dados e defina alguns pontos de quebra em seu código.  
  
5.  Com a processamento de dados extensão projeto janela ainda ativa, clique em **anexar ao processo** no **depurar** menu.  
  
     O **anexar ao processo** caixa de diálogo é aberta.  
  
6.  Na lista de processos, selecione o processo devenv.exe que corresponde ao seu projeto de relatório e clique em **Attach**.  
  
7.  Definir a fonte de dados de relatório usando o **dados de relatório** guia do projeto de relatório. Você provavelmente usará o Designer de Consulta genérico para executar uma consulta na fonte de dados personalizada. Isso deve chamar o depurador e executar o código correspondente a seus pontos de quebra.  
  
8.  Percorra seu código usando a tecla F11. Para obter mais informações sobre como usar o [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] para depuração, consulte a documentação do [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Implantando uma extensão de processamento de dados](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)   
 [Extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementando uma extensão de processamento de dados](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Biblioteca de extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  

