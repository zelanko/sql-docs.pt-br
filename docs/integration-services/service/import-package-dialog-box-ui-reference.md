---
title: "Refer&#234;ncia da interface do usu&#225;rio da caixa de di&#225;logo Importar Pacote | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.dtsserver.importpackage.f1"
helpviewer_keywords: 
  - "Caixa de diálogo Importar Pacote"
ms.assetid: 0e5fb127-c7ff-4dfa-b90e-d9bcf0ce763b
caps.latest.revision: 19
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 19
---
# Refer&#234;ncia da interface do usu&#225;rio da caixa de di&#225;logo Importar Pacote
  Use a caixa de diálogo **Importar Pacote**, disponível no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], para importar um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e para definir ou modificar o nível de proteção do pacote.  
  
## Opções  
 **Local do pacote**  
 Selecione o tipo de local de armazenamento para importar o pacote. As seguintes opções estão disponíveis:  
  
 **SQL Server**  
  
 **Sistema de Arquivos**  
  
 **Armazenamento de Pacotes SSIS**  
  
 **Servidor**  
 Digite um nome de servidor ou selecione um servidor na lista.  
  
 **Autenticação**  
 Selecione a Autenticação do Windows ou a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa opção estará disponível apenas se o local de armazenamento for o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Sempre que for possível, use a Autenticação do Windows.  
  
 **Tipo de autenticação**  
 Selecione um tipo de autenticação.  
  
 **Nome de usuário**  
 Se estiver usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], forneça um nome de usuário.  
  
 **Senha**  
 Se estiver usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], forneça uma senha.  
  
 **Caminho do pacote**  
 Digite o nome do pacote ou clique no botão Procurar **(…)** e localize o pacote.  
  
 **Nome do pacote**  
 Opcionalmente, renomeie o pacote. O nome padrão é o nome do pacote a ser importado.  
  
 **Nível de proteção**  
 Clique no botão Procurar **(…)** e, na caixa de diálogo **Nível de Proteção do Pacote**, atualize o nível de proteção. Para obter mais informações, consulte [Caixa de diálogo Nível de Proteção do Pacote e do Projeto](../../integration-services/packages/package-and-project-protection-level-dialog-box.md).  
  
## Consulte também  
 [Salvar cópia de pacote](../Topic/Save%20Copy%20of%20Package.md)   
 [Referência da interface do usuário da caixa de diálogo Exportar Pacote](../../integration-services/service/export-package-dialog-box-ui-reference.md)   
 [Salvar pacotes](../../integration-services/save-packages.md)   
 [Importar e exportar pacotes &#40;Serviço SSIS&#41;](../../integration-services/service/import-and-export-packages-ssis-service.md)  
  
  