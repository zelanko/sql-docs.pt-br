---
title: Salvar cópia de pacote | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.savecopyas.f1
helpviewer_keywords:
- Save Copy of Package dialog box
ms.assetid: 7b44c0d7-d8fa-4491-8836-0899f621d3a8
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0cd386cad85726707f1ce3ea9f7931bda4e66c25
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48140496"
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
 Digite o caminho do pacote ou clique no botão procurar **(...)** e localize a pasta na qual o pacote será armazenado.  
  
 **Nível de proteção**  
 Clique no botão de procura **(...)** e atualize o nível de proteção na caixa de diálogo **Nível de Proteção do Pacote** . Para obter mais informações, consulte [Caixa de diálogo Nível de Proteção do Pacote e do Projeto](../../2014/integration-services/package-and-project-protection-level-dialog-box.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência de interface do usuário de caixa de diálogo de pacote de importação](../../2014/integration-services/import-package-dialog-box-ui-reference.md)   
 [Referência de interface do usuário da caixa de diálogo pacote de exportação](../../2014/integration-services/export-package-dialog-box-ui-reference.md)   
 [Salvar pacotes](save-packages.md)   
 [Importar e exportar pacotes &#40;serviço SSIS&#41;](../../2014/integration-services/import-and-export-packages-ssis-service.md)  
  
  
