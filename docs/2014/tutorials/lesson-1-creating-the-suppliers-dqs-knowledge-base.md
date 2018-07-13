---
title: 'Lição 1: Criando a Base de dados de conhecimento do DQS fornecedores | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 78825ccb-30fc-463c-8140-435532e2ecd2
caps.latest.revision: 7
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 744658b00253b96bf6110f4382a7a6a8a8d7abfc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37151857"
---
# <a name="lesson-1-creating-the-suppliers-dqs-knowledge-base"></a>Lição 1: Criando a base de dados de conhecimento do DQS de fornecedores
  Nesta lição, você criará uma base de dados de conhecimento do DQS denominada **fornecedores** com o conhecimento (metadados) sobre dados do fornecedor. Use a base de dados de conhecimento para executar as atividades de limpeza e correspondência nos dados do fornecedor de entrada. A atividade de limpeza identifica dados incorretos ou inválidos, corrige os dados incorretos, propõe correções/sugestões, padroniza os dados e enriquece os dados com mais informações. A atividade de correspondência compara dados e identifica registros semelhantes (mas um pouco diferentes) nos dados que o ajudam a remover duplicatas nos dados.  
  
 É possível usar tanto processos interativos quanto processos auxiliados pelo computador para criar, compilar e gerenciar uma base de dados de conhecimento. O conhecimento em uma base de dados de conhecimento é mantido em domínios, cada qual específico para um campo de dados nos dados que você deseja limpar e/ou corresponder.  
  
 Nesta lição, você executará as seguintes tarefas para criar o **fornecedores** da Base de dados de Conhecimento:  
  
-   Criar uma base de dados de conhecimento do DQS denominada **fornecedores**. Você pode criar uma base de dados de conhecimento de várias maneiras. Você pode compilar uma base de dados de conhecimento a partir do zero ou compilá-la a partir de uma base de dados de conhecimento existente ou importando um arquivo DQS (.dqs) que contém uma base de dados de conhecimento pré-compilada e exportada ou uma atividade de descoberta de conhecimento nos dados de exemplo. Neste tutorial, você cria a base de dados de conhecimento do zero.  
  
-   Crie domínios na **fornecedores** base de dados de conhecimento que você use para dados de limpeza e correspondência de dados para identificar duplicatas. Crie domínios para os campos de dados que você deseja usar nas atividades limpeza e correspondência, não para todos os campos de dados nos dados.  
  
-   Adicione valores a um domínio manualmente, importando valores de um arquivo do Excel, executando uma atividade de descoberta de conhecimento nos dados de exemplo e importando valores de projeto de um projeto de limpeza. Você também pode importar valores de domínio importando um arquivo DQS que contém as propriedades e os valores de domínio, que não executa no tutorial.  
  
-   Defina regras para um domínio. Uma regra de domínio é uma condição usada pelo DQS para validar, corrigir e padronizar valores de domínio.  
  
-   Defina relações baseadas em termos para um domínio. Uma relação baseada em termos permite que você faça uma correção para um termo que faz parte de um valor em um domínio. Por exemplo, no valor **Contoso Inc., Inc.** é um termo que pode ser definido como Incorporated. Isso ajuda na padronização dos dados, bem como na identificação de duplicatas. Por exemplo, **Contoso Inc** e **Contoso Incorporated** podem ser considerados duplicatas.  
  
-   Especifique sinônimos em valores de domínio. Você pode definir dois ou mais valores como sinônimos e defini-los como um valor principal, que substitui seus valores de sinônimo durante uma atividade de limpeza para padronizar os dados.  
  
-   Crie um domínio composto denominado Validação de Endereço que inclui os domínios Address Line, City, State e Zip Code. Um domínio composto consiste em um ou mais domínios únicos. Isso permite a você criar uma regra que envolve vários domínios. Por exemplo, você pode definir uma regra: se City for Los Angeles, State deverá ser CA, em que City e State são dois domínios separados.  
  
-   Configure e use um serviço de dados de referência. O recurso Serviço de Dados de Referência no DQS (Data Quality Services) permite a você assinar provedores de dados de referência de terceiros e limpar facilmente e enriquecer os dados empresariais validando-os em relação aos dados de alta qualidade. Você pode usar serviços dos principais provedores DQS de dentro do DQS para padronizar, corrigir ou enriquecer seus dados durante o processo de limpeza. Neste tutorial, você aprenderá a configurar o ambiente do DQS para usar um serviço de dados de referência no Windows Azure Marketplace e usar o serviço associado ao domínio composto Address Validation para limpar dados do endereço.  
  
-   Publique a base de dados de conhecimento para que ela possa ser usada nas atividades de limpeza e correspondência.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 1: Criando a base de dados de conhecimento e domínios](../../2014/tutorials/task-1-creating-a-knowledge-base-and-domains.md)  
  
  
