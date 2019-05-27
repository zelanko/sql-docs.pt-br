---
title: 'Etapa 9: Testar o pacote de tutoriais da Lição 1 | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 9aee7acf-797b-46f2-830d-80ab64a9f0b6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 74099a8611c9c81b54619e1fc071b63a5d22777a
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65722898"
---
# <a name="lesson-1-9-test-the-lesson-1-package"></a>Lição 1-9: Testar o pacote da Lição 1

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



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
  
  
  
