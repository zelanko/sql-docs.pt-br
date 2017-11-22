---
title: "Problemas de Design de segurança do ADO | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: "“drivers”"
ms.topic: article
helpviewer_keywords: ADO, security
ms.assetid: 86b83a38-efdf-4831-a6d5-7e470d517d1c
caps.latest.revision: "18"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fbc093aa095d74831e0f9d75ad78159db2e498e2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="ado-security-design-features"></a>Recursos de Design de segurança do ADO
As seções a seguir descrevem os recursos de design de segurança no ActiveX Data Objects (ADO) 2.8 e posterior. Essas alterações foram feitas no ADO 2.8 para melhorar a segurança. ADO 6.0, que está incluído no Windows DAC 6.0 no Windows Vista, é funcionalmente equivalente ao ADO 2.8, que foi incluído no MDAC 2.8 no Windows XP e Windows Server 2003. Este tópico fornece informações sobre como proteger melhor seus aplicativos no ADO 2.8 ou posterior.

> [!IMPORTANT]
>  Se você estiver atualizando o aplicativo a partir de uma versão anterior do ADO, é recomendável que você teste seu aplicativo atualizado em um computador não seja de produção antes de implantá-lo aos clientes. Dessa forma, você pode garantir que estão cientes dos problemas de compatibilidade antes de implantar seu aplicativo atualizado.

## <a name="internet-explorer-file-access-scenarios"></a>Cenários de acesso de arquivo do Internet Explorer
 O seguinte efeito de recursos como o ADO 2.8 e posterior funciona quando ele é usado em scripts de páginas da Web no Internet Explorer.

### <a name="revised-and-improved-security-warning-message-box-now-used-to-alert-users"></a>Caixa de mensagem de aviso de segurança aprimorada e revisada agora é usada para alertar os usuários
 Para ADO 2.7 e versões anterior, a seguinte mensagem de aviso aparece quando uma página da Web com script tenta executar código ADO de um provedor confiável:

```
This page accesses data on another domain. Do you want to allow this? To
avoid this message in Internet Explorer, you can add a secure Web site to
your Trusted Sites zone on the Security tab of the Internet Options dialog
box.
```

 Para ADO 2.8 e posterior, a mensagem anterior não aparece mais. Em vez disso, a seguinte mensagem aparece neste contexto:

```
This Website uses a data provider that may be unsafe. If you trust the
Website, click OK, otherwise click Cancel.
```

 A mensagem anterior permite que o usuário tomar uma decisão consciente, sabendo as consequências de qualquer opção:

-   Se o site de confiança do usuário, clicando em Okey permitirá que todos os códigos de segurança de disco (todos os métodos de ADO e propriedades com as exceções das APIs do disco acessível descritas mais adiante neste tópico) para executar e executar na janela do navegador.

-   Se o usuário não confia no site, clique em Cancelar bloqueia o código ADO para acesso a dados de execução e a operação em sua totalidade.

### <a name="disk-accessible-code-limited-now-to-trusted-sites"></a>Código acessível ao disco agora limitado aos sites confiáveis
 Foram feitas alterações adicionais no ADO 2.8 especificamente restringir a capacidade de um conjunto limitado de APIs, o que pode expor o potencial para ler ou gravar em arquivos no computador local. Aqui estão os métodos da API que foram mais restrito para fornecer segurança ao executar o Internet Explorer:

-   Para o ADO **fluxo** do objeto, se o [LoadFromFile](../../ado/reference/ado-api/loadfromfile-method-ado.md) ou [SaveToFile](../../ado/reference/ado-api/savetofile-method.md) métodos são usados.

-   Para ADO **Recordset** do objeto, se o [salvar](../../ado/reference/ado-api/save-method.md) método ou o [abrir](../../ado/reference/ado-api/open-method-ado-recordset.md) método, por exemplo, quando qualquer o **adCmdFile** opção está definida ou o [provedor Microsoft OLE DB persistência (MSPersist)](../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md) é usado.

 Para esses conjuntos limitados de funções potencialmente disco acessível, ocorrerá o seguinte comportamento para ADO 2.8 e posterior, se qualquer código que use esses métodos é executado no Internet Explorer:

-   Se o site que forneceu o código foi adicionado anteriormente à lista de zona de Sites confiáveis, o código é executado no navegador e o acesso aos arquivos locais.

-   Se o site não aparecer na lista de zona de Sites confiáveis, o código será bloqueado e é negado acesso a arquivos locais.

    > [!NOTE]
    >  No ADO 2.8 e posterior, o usuário não é alertado ou recomendável para adicionar sites à lista de zona de Sites confiáveis. Portanto, o gerenciamento da lista de Sites confiáveis é responsabilidade daqueles que estão implantando ou oferecer suporte a aplicativos baseados no site da Web que exigem acesso ao sistema de arquivos local.

### <a name="access-blocked-to-the-activecommand-property-on-recordset-objects"></a>Acesso bloqueado para a propriedade ActiveCommand em objetos de conjunto de registros
 Quando executado no Internet Explorer, o ADO 2.8 agora bloqueia o acesso a [ActiveCommand](../../ado/reference/ado-api/activecommand-property-ado.md) propriedade para um ativo **registros** do objeto e retornará um erro. O erro ocorre independentemente se a página é proveniente de um site da Web registrado na lista de Sites confiáveis.

### <a name="changes-in-handling-for-ole-db-providers-and-integrated-security"></a>Alterações na manipulação de provedores OLE DB e a segurança integrada
 Ao revisar ADO 2.7 e versões anteriores para problemas de segurança e problemas potenciais, o cenário a seguir foi descoberto:

 Em alguns casos, os provedores OLE DB que dão suporte a segurança integrada [DBPROP_AUTH_INTEGRATED](https://msdn.microsoft.com/library/windows/desktop/ms712973.aspx) propriedade potencialmente pode permitir script páginas da Web para reutilizar o objeto de Conexão ADO para conectar-se acidentalmente para outros servidores usando as credenciais de logon atual dos usuários. Para evitar isso, o ADO 2.8 e posterior lidar com provedores OLE DB, dependendo de como eles escolhido para fornecer ou não fornecer para a segurança integrada.

 Páginas da Web que são carregadas de sites listados na lista de zona de Sites confiáveis, a tabela a seguir fornece uma análise de como o ADO 2.8 e posterior gerencia conexões ADO em cada caso.

|Configurações do IE para a autenticação de usuário de logon|Provedor dá suporte a "Segurança integrada" e UID e PWD especificado (SQLOLEDB)|Provedor não dá suporte a "Segurança integrada" (JOLT, MSDASQL, MSPersist)|Provedor oferece suporte a "Segurança integrada" e ele é definido como SSPI (nenhum UID/PWD forem especificados)|
|------------------------------------------------|----------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
|Logon automático com o nome de usuário atual e a senha|Permitir conexão|Permitir conexão|Permitir conexão|
|Solicitar nome de usuário e senha|Permitir conexão|Falha de conexão|Falha de conexão|
|Logon automático somente na zona da Intranet|Permitir conexão|Avisar usuário com aviso de segurança|Avisar usuário com aviso de segurança|
|Logon anônimo|Permitir conexão|Falha de conexão|Falha de conexão|

 No caso em que um aviso de segurança agora é exibido, a caixa de mensagem informa os usuários:

```
This Website is using your identity to access a data source. If you trust this Website, click OK, otherwise click Cancel.
```

 A mensagem anterior permite ao usuário tomar uma decisão mais informada e proceda conforme necessário.

> [!NOTE]
>  Para sites confiáveis (ou seja, sites não listados na lista de zona de Sites confiáveis), se o provedor também é não confiável (como discutido anteriormente nesta seção), o usuário verá dois avisos de segurança em uma linha, um aviso sobre o provedor não seguro e um segundo aviso o tentativa de usar a sua identidade. Se o usuário clica Okey para o primeiro aviso, as configurações do Internet Explorer e o código de comportamento de resposta descritos na tabela anterior são executadas.

## <a name="controlling-whether-password-text-is-returned-in-ado-connection-strings"></a>Controlar se o texto da senha é retornado em cadeias de caracteres de conexão ADO
 Ao tentar obter o valor da [ConnectionString](../../ado/reference/ado-api/connectionstring-property-ado.md) propriedade ADO **Conexão** do objeto, os seguintes eventos ocorrem:

1.  Se a conexão estiver aberta, uma chamada de inicialização é feita para o provedor OLE DB subjacente para obter a cadeia de conexão.

2.  Dependendo da configuração no provedor do OLE DB a [DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO](https://msdn.microsoft.com/library/windows/desktop/ms714905.aspx) propriedade, as senhas são incluídas junto com outras informações de cadeia de caracteres de conexão que são retornadas.

 Por exemplo, se a propriedade de Conexão ADO dinâmica **Persist Security Info** é definido como **True**, informações de senha são incluídas na cadeia de conexão retornada. Caso contrário, se o provedor subjacente tiver definido a propriedade como **False** (por exemplo, com o provedor SQLOLEDB), as informações de senha for omitidas na cadeia de conexão retornado.

 Se você estiver usando produtos de terceiros (ou seja, não são da Microsoft) provedores OLE DB com o código do aplicativo ADO, você pode verificar como o **DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO** propriedade é implementada para determinar se a inclusão de informações de senha com cadeias de caracteres de conexão ADO são permitidas.

## <a name="checking-for-non-file-devices-when-loading-and-saving-recordsets-or-streams"></a>Verificando dispositivos diferentes de arquivos ao carregar e salvar fluxos ou conjuntos de registros
 Para ADO 2.7 e versões anterior, arquivo de entrada/saída operações como [abrir](../../ado/reference/ado-api/open-method-ado-recordset.md) e [salvar](../../ado/reference/ado-api/save-method.md) que foram usados para ler e gravar dados com base em arquivo podem em alguns casos permitir um nome de arquivo ou URL a ser usado que especificou um disco não com base em tipo de arquivo. Por exemplo, LPT1, COM2, PRN. TXT, AUX pode ser usado como um alias de entrada/saída entre dispositivos e impressoras auxiliares no sistema usando certos

 Para ADO 2.8 e posterior, essa funcionalidade foi atualizada. Para abrir e salvar **registros** e **fluxo** objetos, ADO executa uma verificação de tipo de arquivo para garantir que o dispositivo de entrada ou de saída especificado em um URL ou nome de arquivo é um arquivo real.

> [!NOTE]
>  Verificação de tipo de arquivo conforme descrito nesta seção se aplica somente para o Windows 2000 e posterior. Ele não se aplica a situações onde ADO 2.8 ou posterior está sendo executado em versões anteriores do Windows, como Windows 98.
