---
title: 'Etapa 5: testar os pacotes atualizados | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 683e52e5-1c7e-49ab-9ffe-6a450a1c5776
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 40884a52395aee9bb45338f5c56d2709f3d4d956
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65722964"
---
# <a name="lesson-1-5---testing-the-updated-packages"></a>Lição 1-5 – testar os pacotes atualizados

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Antes de ir para a próxima lição, na qual você criará o pacote de implantação a ser usado para instalar os pacotes de tutorial no computador de destino, você deverá testar os pacotes. Nesta tarefa, você executará os pacotes, DataTransfer.dtsx e LoadXMLData que você adicionou ao projeto Tutorial de Implantação e então estendeu com configurações.  
  
Quando os pacotes são executados, cada executável do pacote fica com uma cor verde quando concluído com sucesso. Quando todos os executáveis estão verdes, o pacote foi concluído com sucesso. Você também pode visualizar o progresso da execução do pacote na guia **Progresso** .  
  
Se os pacotes não forem executados com sucesso, você precisará corrigi-los antes de ir para a próxima lição.  
  
### <a name="to-run-the-datatransfer-package"></a>Para executar o pacote DataTransfer  
  
1.  No Gerenciador de Soluções, clique em DataTransfer.dtsx.  
  
2.  No menu **Depurar** , clique em **Iniciar Depuração**.  
  
3.  Terminada a execução do pacote, no menu **Depurar** , clique em **Parar Depuração**.  
  
### <a name="to-run-the-loadxmldata-package"></a>Para executar o pacote LoadXMLData  
  
1.  No Gerenciador de Soluções, clique em LoadXMLData.dtsx.  
  
2.  No menu **Depurar** , clique em **Iniciar Depuração**.  
  
3.  Terminada a execução do pacote, no menu **Depurar** , clique em **Parar Depuração**.  
  
## <a name="next-lesson"></a>Próxima lição  
[Lição 2: criar o pacote de implantação no SSIS](../integration-services/lesson-2-create-the-deployment-bundle-in-ssis.md)  
  
  
  
