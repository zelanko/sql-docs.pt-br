---
title: "Refer&#234;ncia da interface do usu&#225;rio da caixa de di&#225;logo Exportar Pacote | Microsoft Docs"
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
  - "sql13.dts.dtsserver.exportpackage.f1"
helpviewer_keywords: 
  - "Caixa de diálogo Exportar Pacote"
ms.assetid: 3742fe8a-ef57-444d-b2fb-cb25d16bae97
caps.latest.revision: 23
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 23
---
# Refer&#234;ncia da interface do usu&#225;rio da caixa de di&#225;logo Exportar Pacote
  Use a caixa de diálogo **Exportar Pacote**, disponível no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], para exportar um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para um local diferente e, opcionalmente, modificar o nível de proteção do pacote.  
  
## Opções  
 **Local do pacote**  
 Selecione o tipo armazenamento para exportar o pacote. As seguintes opções estão disponíveis:  
  
 **SQL Server**  
  
 **Sistema de Arquivos**  
  
 **Armazenamento de Pacotes SSIS **  
  
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
 Digite o caminho do pacote ou clique no botão Procurar **(…)** e localize a pasta na qual o pacote será armazenado.  
  
 **Nível de proteção**  
 Clique no botão Procurar **(…)** e atualize o nível de proteção na caixa de diálogo **Nível de Proteção do Pacote**. Para obter mais informações, consulte [Caixa de diálogo Nível de Proteção do Pacote e do Projeto](../../integration-services/packages/package-and-project-protection-level-dialog-box.md).  
  
## Consulte também  
 [Salvar cópia de pacote](../Topic/Save%20Copy%20of%20Package.md)   
 [Referência da interface do usuário da caixa de diálogo Importar Pacote](../../integration-services/service/import-package-dialog-box-ui-reference.md)   
 [Salvar pacotes](../../integration-services/save-packages.md)   
 [Importar e exportar pacotes &#40;Serviço SSIS&#41;](../../integration-services/service/import-and-export-packages-ssis-service.md)  
  
  