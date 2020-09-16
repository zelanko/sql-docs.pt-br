---
description: Proteger pastas
title: Proteger pastas | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- high-security folders [Reporting Services]
- low-security folders
- folders [Reporting Services], security
- security [Reporting Services], folders
ms.assetid: 0fd91f77-0143-476b-9af0-87293be78e44
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f873c02fe9cf0657edbaefd7411b6f3409ed1a0d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88497999"
---
# <a name="secure-folders"></a>Proteger pastas
  A segurança de pasta é a base para proteger todo o conteúdo em um servidor de relatório. Como a segurança é herdada em toda a estrutura de pastas, é possível designar seções grandes ou pequenas da hierarquia de pasta para permitir determinados tipos de acesso.  
  
 As pastas de alta segurança podem ser usadas para armazenar relatórios confidenciais ou como áreas de preparação; por exemplo, você pode ter uma pasta usada para testar os relatórios antes de movê-los para um local final. Para controlar o acesso a essa área, você pode definir uma atribuição de função que permite somente aos autores de relatório adicionar e excluir itens e uma segunda atribuição de função que permite aos testadores executar relatórios, mas não adicionar ou remover itens. Como as atribuições de função são definidas explicitamente para testadores e autores de relatório, nenhum outro usuário (exceto os administradores do sistema local) pode acessar a pasta.  
  
 As pastas de baixa segurança podem ser usadas para armazenar relatórios que você deseja acessar com facilidade.  
  
 A segurança de pasta é a base da segurança no nível do item, começando com o nó raiz da hierarquia de pastas do servidor de relatório, a pasta Base. Como segurança é herdada, é aconselhável definir uma política de segurança bastante restritiva na pasta Base. Usar a função **Navegador** nas atribuições de função da pasta Base é exatamente o mesmo que fornecer o acesso somente exibição.  
  
## <a name="tasks-and-folder-access"></a>Tarefas e acesso à pasta  
 Ao criar atribuições de função para pastas, considere as tarefas listadas na tabela a seguir.  
  
|Selecione esta tarefa|Para dar permissão para|  
|----------------------|---------------------------|  
|Exibir pastas|Exibir a hierarquia de pastas e as propriedades somente leitura que indicam quando a pasta foi criada e modificada.<br /><br /> Os usuários não podem exibir itens na pasta, a não ser que obtenham funções que também incluem as seguintes tarefas: “Exibir relatórios”, “Exibir modelos”, “Exibir recursos” e “Exibir fontes de dados”.|  
|Gerenciar pastas|Exibir propriedades de pasta, alterar o nome ou a descrição ou mover a pasta para outro local. Essa tarefa permite que os usuários criem pastas.|  
|Gerenciar relatórios|Adicionar relatórios do sistema de arquivos a uma pasta e publicar relatórios do Designer de Relatórios no servidor de relatório.|  
|Gerenciar as fontes de dados|Adicionar novos itens de fontes de dados compartilhadas a uma pasta e alterar as fontes de dados compartilhadas existentes.|  
|Definir segurança em itens|Criar e modificar atribuições de função que controlam o acesso à pasta. Essa tarefa deve ser usada com “Exibir pastas” ou “Gerenciar pastas”. Se não for, não terá nenhum efeito porque o usuário não poderá selecionar o item.|  
  
## <a name="see-also"></a>Consulte Também  
 [Proteger relatórios e recursos](../../reporting-services/security/secure-reports-and-resources.md)   
 [Proteger itens de fontes de dados compartilhadas](../../reporting-services/security/secure-shared-data-source-items.md)   
 [Conceder permissões em um servidor de relatório no Modo Nativo](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
