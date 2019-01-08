---
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
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 3fd443ff2ad58aa503fac2960016cb55f35b8a7f
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52514945"
---
# <a name="creating-test-cases-sybasetosql"></a>Criar casos de teste (SybaseToSQL)
Use o Assistente de caso de teste para criar um teste. Este assistente permite criar casos de teste escolhendo testados e verificados os objetos e especificando os parâmetros de testes.  
  
## <a name="starting-the-test-case-wizard"></a>Iniciando o Assistente de caso de teste  
Para iniciar o Assistente de caso de teste, clique em **novo caso de teste...**  do **testador** menu.  
  
Quando iniciado, o assistente procura ssmatester2005db de banco de dados ou ssmatester2008db (dependendo do tipo de projeto) no servidor de origem de Sybase. É o esquema de extensão do testador usado para armazenar objetos auxiliares. Se o Assistente de caso de teste não é possível localizar ssmatester2005db ou ssmatester2008db, ele exibirá uma janela de caixa de diálogo que propõe para criar o banco de dados de extensão do testador. (Essa situação geralmente ocorre durante a primeira execução do SSMA testador).  
  
Se você receber a janela de diálogo, clique em **Sim** para criar o banco de dados do Sybase testador no servidor de origem. Em seguida, uma nova janela de caixa de diálogo será exibida em que você deve adicionar um ou mais dispositivos na qual localizar o novo banco de dados do testador. Clique em **adicionar** para adicionar um dispositivo. No **alocação de espaço para o banco de dados do testador** caixa de diálogo, escolha o dispositivo e especificar o tamanho usado pelo banco de dados do testador. Além disso, você pode definir o dispositivo separado para logs de banco de dados. Observe que você deve ter privilégios de Sybase para criar bancos de dados.  
  
## <a name="overview-of-creating-test-cases-using-the-wizard"></a>Visão geral da criação de casos de teste usando o Assistente  
O processo de criação de um caso de teste consiste em cinco etapas:  
  
1.  [Inicializar casos de teste &#40;SybaseToSQL&#41;](../../ssma/sybase/initializing-test-cases-sybasetosql.md).  
  
2.  [Selecionando e Configurando objetos a testar &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-objects-to-test-sybasetosql.md).  
  
3.  [Selecionar e configurar os objetos afetados pelo &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md).  
  
4.  [Personalizando a ordem das chamadas &#40;SybaseToSQL&#41;](../../ssma/sybase/customizing-calls-order-sybasetosql.md).  
  
5.  [Concluir a preparação do caso de teste &#40;SybaseToSQL&#41;](../../ssma/sybase/finishing-test-case-preparation-sybasetosql.md).  
  
## <a name="see-also"></a>Consulte também  
[Testar objetos de banco de dados migrados &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
