---
title: Importar a referência de interface do usuário da caixa de diálogo pacote | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.dtsserver.importpackage.f1
helpviewer_keywords:
- Import Package dialog box
ms.assetid: 0e5fb127-c7ff-4dfa-b90e-d9bcf0ce763b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2631235c2ed0011aca4e734c7a61093203518636
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58377934"
---
# <a name="import-package-dialog-box-ui-reference"></a>Referência da interface do usuário da caixa de diálogo Importar Pacote
  Use a caixa de diálogo **Importar Pacote**, disponível no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], para importar um pacote do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e para definir ou modificar o nível de proteção do pacote.  
  
## <a name="options"></a>Opções  
 **Local do pacote**  
 Selecione o tipo de local de armazenamento para importar o pacote. As seguintes opções estão disponíveis:  
  
 **SQL Server**  
  
 **Sistema de Arquivos**  
  
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
 Digite o nome do pacote ou clique no botão Procurar **(…)** e localize o pacote.  
  
 **Nome do pacote**  
 Opcionalmente, renomeie o pacote. O nome padrão é o nome do pacote a ser importado.  
  
 **Nível de proteção**  
 Clique no botão Procurar **(…)** e, na caixa de diálogo **Nível de Proteção do Pacote**, atualize o nível de proteção. Para obter mais informações, consulte [Caixa de diálogo Nível de Proteção do Pacote e do Projeto](../../2014/integration-services/package-and-project-protection-level-dialog-box.md).  
  
## <a name="see-also"></a>Consulte também  
 [Salvar cópia de pacote](../../2014/integration-services/save-copy-of-package.md)   
 [Referência da interface do usuário da caixa de diálogo Exportar Pacote](../../2014/integration-services/export-package-dialog-box-ui-reference.md)   
 [Salvar pacotes](save-packages.md)   
 [Importar e exportar pacotes &#40;Serviço SSIS&#41;](../../2014/integration-services/import-and-export-packages-ssis-service.md)  
  
  
