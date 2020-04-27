---
title: Referência da interface do usuário da caixa de diálogo Exportar pacote | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.dtsserver.exportpackage.f1
helpviewer_keywords:
- Export Package dialog box
ms.assetid: 3742fe8a-ef57-444d-b2fb-cb25d16bae97
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c1cca0a2761f87d6f4f3837df1e9a0bdcc5b91a4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66058907"
---
# <a name="export-package-dialog-box-ui-reference"></a>Referência da interface do usuário da caixa de diálogo Exportar Pacote
  Use a caixa de diálogo **Exportar Pacote** , disponível no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], para exportar um pacote do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para um local diferente e, opcionalmente, modificar o nível de proteção do pacote.  
  
## <a name="options"></a>Opções  
 **Local do pacote**  
 Selecione o tipo armazenamento para exportar o pacote. As seguintes opções estão disponíveis:  
  
 **SQL Server**  
  
 **Sistema de arquivos**  
  
 **Armazenamento de Pacotes SSIS**  
  
 **Servidor**  
 Digite um nome de servidor ou selecione um servidor na lista.  
  
 **Autenticação**  
 Selecione a Autenticação do Windows ou a Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Essa opção estará disponível apenas se o local de armazenamento for o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Sempre que for possível, use a Autenticação do Windows.  
  
 **Tipo de autenticação**  
 Selecione um tipo de autenticação.  
  
 **Nome de usuário**  
 Se estiver usando a Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , forneça um nome de usuário.  
  
 **Senha**  
 Se estiver usando a Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , forneça uma senha.  
  
 **Caminho do pacote**  
 Digite o caminho do pacote ou clique no botão procurar **(...)** e localize a pasta na qual armazenar o pacote.  
  
 **Nível de proteção**  
 Clique no botão procurar **(...)** e atualize o nível de proteção na caixa de diálogo **nível de proteção do pacote** . Para obter mais informações, consulte [Caixa de diálogo Nível de Proteção do Pacote e do Projeto](../../2014/integration-services/package-and-project-protection-level-dialog-box.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Salvar cópia do pacote](../../2014/integration-services/save-copy-of-package.md)   
 [Referência da interface do usuário da caixa de diálogo Importar pacote](../../2014/integration-services/import-package-dialog-box-ui-reference.md)   
 [Salvar pacotes](save-packages.md)   
 [Importar e exportar pacotes &#40;Serviço SSIS&#41;](../../2014/integration-services/import-and-export-packages-ssis-service.md)  
  
  
