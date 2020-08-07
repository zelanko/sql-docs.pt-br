---
title: Configurações de migração de dados (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 91f7f558-025d-4f4d-ac2c-aa095e7d1ace
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: b86114566be6b560aa571f15af1e3dfac3e59501
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87934874"
---
# <a name="data-migration-settings-oracletosql"></a>Configurações de migração de dados (OracleToSQL)
  
## <a name="data-migration-settings"></a>Configurações de migração de dados  
**As configurações de migração de dados** permitem que o usuário grave consultas personalizadas para migração de dados.  
  
-   Essa guia está disponível quando **as opções de migração de dados estendidas** estão definidas para **Mostrar** e ficam ocultas quando a configuração é definida como **ocultar** nas configurações do projeto. Para obter mais informações sobre as configurações de migração do projeto, consulte [configurações do projeto (migração)](https://msdn.microsoft.com/fcd6b988-633b-4b2b-9f36-6368b5e86b60) .  
  
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
[Migrando dados do Oracle para SQL Server](migrating-oracle-data-into-sql-server-oracletosql.md)  
  
