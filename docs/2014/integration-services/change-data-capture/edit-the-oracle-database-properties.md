---
title: Editar as propriedades do banco de dados Oracle | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- oraProp
ms.assetid: 58dc99f1-ee6b-4508-bb66-2bc589611ff7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c9ebad419585de0136708ea85e522f890dceac38
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62835572"
---
# <a name="edit-the-oracle-database-properties"></a>Editar as propriedades do banco de dados Oracle
  Use a guia Oracle no editor de Propriedades para fazer alterações na descrição fornecida na página Create CDC database no assistente de Nova Instância e fazer alterações nas informações de conexão de banco de dados de mineração de logs do Oracle.  
  
 Veja a seguir a descrição das informações na guia **Oracle** .  
  
 **Nome**  
 O nome da Instância CDC inserido na página Create CDC Database no New Instance Wizard. Este campo é somente leitura e você não pode editar essas informações.  
  
 **Descrição**  
 Você pode editar a descrição da nova instância ou adicionar uma se não tiver feito, ao criar a Instância CDC.  
  
 **Cadeia de conexão do Oracle**  
 A cadeia de conexão do Oracle no computador com o banco de dados Oracle que você está usando. Este campo é somente leitura e você não pode editar essas informações. Isto ocorre porque algumas alterações na cadeia de conexão podem apontar a Instância Oracle CDC para outro banco de dados Oracle inteiramente, corrompendo o estado da Instância CDC armazenada na tabela **cdc.xdbcdc_config** . Se for necessário realizar alterações secundárias, você poderá alterar a cadeia de conexão diretamente na tabela de configuração usando o SQL Server Management Studio.  
  
 **Autenticação de mineração de logs da Oracle**  
 Para inserir as credenciais de autenticação para o banco de dados Oracle que contém o minerador de logs, siga um destes procedimentos em **Autenticação**:  
  
-   **Autenticação do Windows**: selecione isto para usar as credenciais de domínio atuais do Windows. Você só poderá usar esta opção se o banco de dados Oracle estiver configurado para funcionar com autenticação do Windows.  
  
-   **Autenticação do Oracle**: se você selecionou esta opção, deve digitar o **Nome de usuário** e **Senha** para o usuário no banco de dados Oracle ao qual você está se conectando.  
  
 Você pode ver as propriedades do banco de dados Oracle no visualizador. Ao usar o visualizador, as informações serão somente leitura. O visualizador também inclui uma lista das colunas capturadas na tabela. Para obter mais informações sobre como acessar o visualizador, consulte [How to Manage a CDC Instance](manage-a-cdc-instance.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Como gerenciar um serviço CDC no CDC Designer Console](how-to-manage-a-cdc-service-from-the-cdc-designer-console.md)   
 [Conectar-se a um banco de dados de origem Oracle](connect-to-an-oracle-source-database.md)   
 [Conectar-se ao Oracle](connect-to-oracle.md)  
  
  
