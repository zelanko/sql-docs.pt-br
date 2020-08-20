---
description: Criar casos de teste (SybaseToSQL)
title: Criando casos de teste (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester component,Test Case Wizard
ms.assetid: b52dfd93-95af-4299-bc8f-83f2a7a6a518
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: fb3fe4816faeb050a1c4321def0e7dd4e6937bdb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463148"
---
# <a name="creating-test-cases-sybasetosql"></a>Criar casos de teste (SybaseToSQL)
Use o assistente de caso de teste para criar um teste. Este assistente permite que você crie casos de teste escolhendo objetos testados e verificados e especificando os parâmetros de teste.  
  
## <a name="starting-the-test-case-wizard"></a>Iniciando o assistente de caso de teste  
Para iniciar o assistente de caso de teste, clique em **novo caso de teste...** no menu **testador** .  
  
Quando iniciado, o assistente procura o banco de dados ssmatester2005db ou ssmatester2008db (dependendo do tipo de projeto) no servidor Sybase de origem. É o esquema de extensão do testador usado para armazenar objetos auxiliares. Se o assistente de caso de teste não conseguir localizar ssmatester2005db ou ssmatester2008db, ele exibirá uma janela de diálogo que propõe criar o banco de dados de extensão do testador. (Essa situação geralmente ocorre durante a primeira execução do SSMA Tester.)  
  
Se você receber a janela de diálogo, clique em **Sim** para criar o banco de dados do Sybase Tester no servidor de origem. Em seguida, uma nova janela de diálogo será exibida onde você deve adicionar um ou mais dispositivos nos quais localizar o novo banco de dados de testador. Clique em **Adicionar** para adicionar um dispositivo. Na caixa de diálogo **espaço de alocação para banco de dados do testador** , escolha o dispositivo e especifique o tamanho usado pelo banco de dados do testador. Além disso, você pode definir o dispositivo separado para logs de banco de dados. Observe que você deve ter privilégios de Sybase para criar bancos de dados.  
  
## <a name="overview-of-creating-test-cases-using-the-wizard"></a>Visão geral da criação de casos de teste usando o assistente  
O processo de criação de um caso de teste consiste em cinco etapas:  
  
1.  [Inicializando casos de teste &#40;SybaseToSQL&#41;](../../ssma/sybase/initializing-test-cases-sybasetosql.md).  
  
2.  [Seleção e configuração de objetos para testar &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-objects-to-test-sybasetosql.md).  
  
3.  [Selecionando e configurando objetos afetados &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md).  
  
4.  [Personalizando a ordem das chamadas &#40;SybaseToSQL&#41;](../../ssma/sybase/customizing-calls-order-sybasetosql.md).  
  
5.  [Concluindo a preparação do caso de teste &#40;SybaseToSQL&#41;](../../ssma/sybase/finishing-test-case-preparation-sybasetosql.md).  
  
## <a name="see-also"></a>Consulte Também  
[Testando objetos de banco de dados migrados &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
