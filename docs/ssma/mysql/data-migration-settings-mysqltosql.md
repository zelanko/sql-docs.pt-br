---
description: Configurações de migração de dados (MySQLToSQL)
title: Configurações de migração de dados (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9c396df4-5676-4f32-9c57-70d4f15f9b7a
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 3bc5427d17a8678e81ee148d247d743bda9d53ff
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988712"
---
# <a name="data-migration-settings-mysqltosql"></a>Configurações de migração de dados (MySQLToSQL)
  
## <a name="data-migration-settings"></a>Configurações de migração de dados  
**As configurações de migração de dados** permitem que o usuário grave consultas personalizadas para migração de dados.  
  
-   Essa guia está disponível quando **as opções de migração de dados estendidas** estão definidas para **Mostrar** e ficam ocultas quando a configuração é definida como **ocultar** nas configurações do projeto. Para obter mais informações sobre as configurações de migração do projeto, consulte [configurações do projeto (migração)](./project-settings-migration-mysqltosql.md) .  
  
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
[Migrando dados do MySQL para SQL Server/SQL Azure](./migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
