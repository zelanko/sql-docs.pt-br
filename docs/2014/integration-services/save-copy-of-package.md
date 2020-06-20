---
title: Salvar cópia do pacote | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.savecopyas.f1
helpviewer_keywords:
- Save Copy of Package dialog box
ms.assetid: 7b44c0d7-d8fa-4491-8836-0899f621d3a8
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 29e6b0cfe7d7646b317073298410c479c2cd5665
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84964301"
---
# <a name="save-copy-of-package"></a>Salvar cópia de pacote
  Use a caixa de diálogo **Salvar Cópia de Pacote** , disponível no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], para salvar a cópia de um pacote [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] do [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] em um local diferente e, opcionalmente, modificar o nível de proteção do pacote.  
  
## <a name="options"></a>Opções  
 **Local do pacote**  
 Selecione o tipo de local de armazenamento no qual a cópia do pacote será salva. As seguintes opções estão disponíveis:  
  
 **SQL Server**  
  
 **Sistema de Arquivos**  
  
 **Armazenamento de Pacotes SSIS**  
  
 **Servidor**  
 Digite um nome de servidor ou selecione um servidor na lista. Essa opção só estará disponível se o local de armazenamento for **SQL Server** ou **Armazenamento de Pacotes SSIS**.  
  
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
 [Referência da interface do usuário da caixa de diálogo Importar pacote](../../2014/integration-services/import-package-dialog-box-ui-reference.md)   
 [Referência da interface do usuário da caixa de diálogo Exportar pacote](../../2014/integration-services/export-package-dialog-box-ui-reference.md)   
 [Salvar pacotes](save-packages.md)   
 [Importar e exportar pacotes &#40;Serviço SSIS&#41;](../../2014/integration-services/import-and-export-packages-ssis-service.md)  
  
  
