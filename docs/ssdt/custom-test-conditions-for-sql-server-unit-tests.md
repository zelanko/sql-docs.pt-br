---
title: Condições de teste personalizadas para testes de unidade do SQL Server
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 32a15d61-e908-4ae1-a238-4fd0f988d8c8
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 2852d075b6d5b1f55b76fea6b32443ea14e74384
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75245527"
---
# <a name="custom-test-conditions-for-sql-server-unit-tests"></a>Condições de teste personalizadas para testes de unidade do SQL Server

Você pode adicionar condições de teste personalizadas para testes de unidade do SQL Server. No entanto, você deve primeiro instalar a condição de teste antes de usá-la, se criou a extensão ou se estiver instalando uma que alguém criou.  
  
Antes de instalar uma condição de teste que não criou, você deverá entender os seguintes riscos:  
  
-   O programa de instalação para a condição de teste pode ser malicioso e obter acesso a recursos protegidos baseado nas suas permissões de instalação.  
  
-   A própria condição de teste pode ser maliciosa e obter controle de recursos protegidos se quem usar a extensão tiver permissões suficientes.  
  
Para minimizar o risco, você deverá instalar uma condição de teste personalizada somente se for de uma origem conhecida. Se você obtiver uma condição de teste de uma origem não confiável, deverá inspecionar o código-fonte para essa condição de teste e seu programa de instalação (se houver) antes de instalá-lo.  
  
Para instalar uma condição de teste personalizada, copie o assembly assinado (.dll) para %Arquivos de Programas%\Microsoft Visual Studio <Version>\Common7\IDE\Extensions\Microsoft\SQLDB\TestConditions folder. Se esta pasta não existir, crie-a. Você precisa de privilégios administrativos em seu computador para copiar para este diretório.  
  
> [!NOTE]  
> Você precisa instalar as versões do Visual Studio 2010 e Visual Studio 2012 da condição de teste se,  
>   
> -   Você instalar condições de teste personalizadas em um computador que pode ser usado para criar testes de unidade do SQL Server.  
> -   Esses testes de unidade forem usados no Visual Studio 2010 e no Visual Studio 2012.  
  
Para saber mais sobre condições de teste personalizadas para os testes de unidade do SQL Server, confira:  
  
-   [Como criar condições de teste para o designer de teste de unidade do SQL Server](../ssdt/how-to-create-test-conditions-for-the-sql-server-unit-test-designer.md)  
  
-   [Como atualizar uma condição de teste personalizada do Visual Studio 2010 de uma versão anterior do SQL Server Data Tools](../ssdt/how-to-upgrade-visual-studio-2010-custom-test-condition-to-ssdt.md)  
  
-   [Passo a passo: usar uma condição de teste personalizada para verificar os resultados de um procedimento armazenado](../ssdt/walkthrough-use-custom-test-condition-to-verify-stored-procedure-results.md)  
  
## <a name="see-also"></a>Consulte Também  
[Verificar o código do banco de dados usando os testes de unidade do SQL Server](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
  
