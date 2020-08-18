---
description: Configurações de migração de dados (SybaseToSQL)
title: Configurações de migração de dados (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 94d7a083-2dbc-4e3d-94dd-92b7ff9d0c2d
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 1d86fbfceefd3f0a4fba6f3bb86a071736e12c54
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492230"
---
# <a name="data-migration-settings-sybasetosql"></a>Configurações de migração de dados (SybaseToSQL)
  
## <a name="data-migration-settings"></a>Configurações de migração de dados  
**As configurações de migração de dados** permitem que o usuário grave consultas personalizadas para migração de dados.  
  
-   Essa guia está disponível quando **as opções de migração de dados estendidas** estão definidas para **Mostrar** e ficam ocultas quando a configuração é definida como **ocultar** nas configurações do projeto. Para obter mais informações sobre as configurações de migração do projeto, consulte [configurações do projeto (migração)](https://msdn.microsoft.com/82f8857f-7ab1-4738-ab6e-b1e95ea94924) .  
  
-   A análise de instruções SQL personalizadas será implementada na guia **configurações de migração de dados** do nó da tabela.  
  
-   A seguir estão as duas caixas de seleção disponíveis nas **configurações de migração de dados** aula sobre visualização.:  
  
    1.  Truncar SQL Server tabela  
  
    2.  Usar seleção personalizada  
  
1.  **Truncar SQL Server tabela:**  
     Essa opção permite que o usuário tenha uma exibição clara dos dados migrados no banco de dado de destino.  
  
    -   Por padrão, essa caixa de texto é marcada.  
  
    -   Se essa caixa de texto estiver desmarcada, os dados que são migrados serão adicionados aos dados existentes no banco de dado de destino.  
  
2.  **Usar seleção personalizada:**  
     Essa opção permite que o usuário modifique a instrução **Select** presente (a instrução**Select** permite que os usuários selecionem os dados a serem exibidos no banco de dado de destino).  
  
    1.  Por padrão, essa caixa de texto está desmarcada.  
  
    2.  Se essa caixa de texto estiver marcada, ela permitirá que os usuários modifiquem a instrução **Select** presente.  
  
Há dois botões presentes aula sobre visualização.:  
  
-   **Aplicar:** Clique em **aplicar** para aplicar as configurações que foram alteradas.  
  
-   **Cancelar:** Clique em **Cancelar** para restaurar as configurações presentes antes que as alterações tenham sido feitas.  
  
## <a name="see-also"></a>Consulte Também  
[Migrando dados do Sybase para o SQL Server/SQL Azure](https://msdn.microsoft.com/54a39f5e-9250-4387-a3ae-eae47c799811)  
  
