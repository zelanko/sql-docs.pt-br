---
description: 'Etapa 9: Testar o pacote de tutorial da Lição 1'
title: 'Etapa 9: Testar o pacote de tutoriais da Lição 1 | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 9aee7acf-797b-46f2-830d-80ab64a9f0b6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 758f5e0c312afc2a8310743f917cc00a1c43462c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88462002"
---
# <a name="lesson-1-9-test-the-lesson-1-package"></a>Lição 1-9: Testar o pacote da Lição 1

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



Neste tutorial, você executou as seguintes tarefas:  
  
-   Criou um novo projeto do [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
-   Configurou os gerenciadores de conexões para o pacote para estabelecer conexão com os dados de origem e de destino.  
  
-   Adicionou um fluxo de dados que usa os dados de uma origem de arquivo simples, desenvolve as transformações Pesquisa necessárias sobre os dados e configura os dados para o destino.  
  
Seu pacote agora está concluído e pronto para testar!
  
## <a name="check-the-package-components"></a>Verificar os componentes de pacote
  
Antes de testar o pacote, verifique se os fluxos de controle e de dados do pacote da Lição 1 contêm os objetos mostrados nos diagramas a seguir.  
  
**Fluxo de Controle** 
  
![Fluxo de controle no pacote](../integration-services/media/task9lesson1control.gif "Fluxo de controle no pacote")  
  
**Fluxo de Dados**  
  
![Fluxo de dados no pacote](../integration-services/media/task9lesson1data.gif "Fluxo de dados no pacote")  
  
## <a name="run-the-lesson-1-package"></a>Executar o pacote da Lição 1  
  
1.  No menu **Depurar**, selecione **Iniciar Depuração**.  
  
    O pacote é executado, resultando na adição bem-sucedida de 1.097 linhas à tabela de fatos **NewFactCurrencyRate** em **AdventureWorksDW2012**. Para verificar esse resultado, selecione a guia **Fluxo de Dados**.
  
2.  Terminada a execução do pacote, no menu **Depurar**, selecione **Parar Depuração**.  
  
## <a name="go-to-next-lesson"></a>Vá para a próxima lição
[Lição 2: Adicionar looping com o SSIS](../integration-services/lesson-2-adding-looping-with-ssis.md)  
  
## <a name="see-also"></a>Confira também  
[Execução de projetos e pacotes](packages/run-integration-services-ssis-packages.md) 
  
  
  
