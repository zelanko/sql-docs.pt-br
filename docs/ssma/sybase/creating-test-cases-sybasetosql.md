---
title: Criar casos de teste (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Tester component,Test Case Wizard
ms.assetid: b52dfd93-95af-4299-bc8f-83f2a7a6a518
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 54eda3b9434d52e221c7223e87c1305adc3d125c
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34778412"
---
# <a name="creating-test-cases-sybasetosql"></a>Criar casos de teste (SybaseToSQL)
Use o Assistente de caso de teste para criar um teste. Este assistente permite que você crie casos de teste escolhendo testados e verificados os objetos e especificando os parâmetros de teste.  
  
## <a name="starting-the-test-case-wizard"></a>Iniciar o Assistente de caso de teste  
Para iniciar o clique do Assistente de caso de teste **novo caso de teste...** do **Tester** menu.  
  
Quando iniciado, o assistente procura ssmatester2005db de banco de dados ou ssmatester2008db (dependendo do tipo de projeto) no servidor do Sybase de origem. É o esquema de extensão de teste usado para armazenar objetos auxiliares. Se o Assistente de caso de teste não é possível localizar ssmatester2005db ou ssmatester2008db, ele exibe uma janela de diálogo que propõe para criar o banco de dados de extensão de teste. (Essa situação normalmente ocorre durante a primeira execução do SSMA Tester).  
  
Se você abrir a janela de diálogo, clique em **Sim** para criar o banco de dados do Sybase tester no servidor de origem. Em seguida, uma nova janela de diálogo será exibida em que você deve adicionar um ou mais dispositivos no qual localizar o novo banco de dados de teste. Clique em **adicionar** para adicionar um dispositivo. No **alocação de espaço para o banco de dados de teste** caixa de diálogo Escolher o dispositivo e especifique o tamanho usado pelo banco de dados de teste. Além disso, você pode definir o dispositivo separado para os logs de banco de dados. Observe que você deve ter privilégios de Sybase para criar bancos de dados.  
  
## <a name="overview-of-creating-test-cases-using-the-wizard"></a>Visão geral de casos de teste usando o Assistente de criação  
O processo de criação de um caso de teste consiste em cinco etapas:  
  
1.  [Inicializando os casos de teste &#40;SybaseToSQL&#41;](../../ssma/sybase/initializing-test-cases-sybasetosql.md).  
  
2.  [Selecionando e Configurando objetos para teste &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-objects-to-test-sybasetosql.md).  
  
3.  [Selecionar e configurar objetos afetados &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md).  
  
4.  [Personalizando a ordem de chamadas &#40;SybaseToSQL&#41;](../../ssma/sybase/customizing-calls-order-sybasetosql.md).  
  
5.  [Concluindo a preparação do caso de teste &#40;SybaseToSQL&#41;](../../ssma/sybase/finishing-test-case-preparation-sybasetosql.md).  
  
## <a name="see-also"></a>Consulte também  
[Teste de objetos de banco de dados migrados &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
