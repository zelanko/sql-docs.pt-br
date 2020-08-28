---
description: Escrever seu próprio manipulador personalizado
title: Escrevendo seu próprio manipulador personalizado | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory handler in RDS [ADO]
- customized handler in RDS [ADO]
ms.assetid: d447712a-e123-47b5-a3a4-5d366cfe8d72
author: rothja
ms.author: jroth
ms.openlocfilehash: e421b128faa5a7d90ec658a7c42e246110d921fb
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88977337"
---
# <a name="writing-your-own-customized-handler"></a>Escrever seu próprio manipulador personalizado
Talvez você queira escrever seu próprio manipulador se você for um administrador do servidor IIS que deseja o suporte do RDS padrão, mas mais controle sobre as solicitações de usuário e os direitos de acesso.  
  
 O MSDFMAP. O manipulador implementa a interface **IDataFactoryHandler** .  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="idatafactoryhandler-interface"></a>Interface IDataFactoryHandler  
 Essa interface tem dois métodos, **GetRecordset** e **reconnect**. Ambos os métodos exigem que a propriedade [CursorLocation](../../reference/ado-api/cursorlocation-property-ado.md) seja definida como **adUseClient**.  
  
 Ambos os métodos usam argumentos que aparecem após a primeira vírgula na palavra-chave "**Handler =**". Por exemplo, `"Handler=progid,arg1,arg2;"` passará uma cadeia de argumentos de `"arg1,arg2"` e `"Handler=progid"` passará um argumento nulo.  
  
## <a name="getrecordset-method"></a>Método GetRecordset  
 Esse método consulta a fonte de dados e cria um novo objeto [Recordset](../../reference/ado-api/recordset-object-ado.md) usando os argumentos fornecidos. O **conjunto de registros** deve ser aberto com **adLockBatchOptimistic** e não deve ser aberto de forma assíncrona.  
  
### <a name="arguments"></a>Argumentos  
 ***Conn***  A cadeia de conexão.  
  
 ***argumentos***  Os argumentos para o manipulador.  
  
 ***consulta***  do  O texto do comando para fazer uma consulta.  
  
 ***ppRS***  O ponteiro onde o **conjunto de registros** deve ser retornado.  
  
## <a name="reconnect-method"></a>Reconectar método  
 Esse método atualiza a fonte de dados. Ele cria um novo objeto de [conexão](../../reference/ado-api/connection-object-ado.md) e anexa o **conjunto de registros**fornecido.  
  
### <a name="arguments"></a>Argumentos  
 ***Conn***  A cadeia de conexão.  
  
 ***argumentos***  Os argumentos para o manipulador.  
  
 ***pRS***  Um objeto **Recordset** .  
  
## <a name="msdfhdlidl"></a>msdfhdl. idl  
 Essa é a definição de interface para **IDataFactoryHandler** que aparece no arquivo **msdfhdl. idl** .  
  
```cpp
[  
  uuid(D80DE8B3-0001-11d1-91E6-00C04FBBBFB3),  
  version(1.0)  
]  
library MSDFHDL  
{  
    importlib("stdole32.tlb");  
    importlib("stdole2.tlb");  
  
    // TLib : Microsoft ActiveX Data Objects 2.0 Library  
    // {00000200-0000-0010-8000-00AA006D2EA4}  
    #ifdef IMPLIB  
    importlib("implib\\x86\\release\\ado\\msado15.dll");  
    #else  
    importlib("msado20.dll");  
    #endif  
  
    [  
      odl,  
      uuid(D80DE8B5-0001-11d1-91E6-00C04FBBBFB3),  
      version(1.0)  
    ]  
    interface IDataFactoryHandler : IUnknown  
    {  
HRESULT _stdcall GetRecordset(  
      [in] BSTR conn,  
      [in] BSTR args,  
      [in] BSTR query,  
      [out, retval] _Recordset **ppRS);  
  
// DataFactory will use the ActiveConnection property  
// on the Recordset after calling Reconnect.  
   HRESULT _stdcall Reconnect(  
      [in] BSTR conn,  
      [in] BSTR args,  
      [in] _Recordset *pRS);  
    };  
};  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Seção conexão de arquivo de personalização](./customization-file-connect-section.md)   
 [Seção de logs de arquivo de personalização](./customization-file-logs-section.md)   
 [Seção SQL do arquivo de personalização](./customization-file-sql-section.md)   
 [Seção UserList do arquivo de personalização](./customization-file-userlist-section.md)   
 [Personalização de datafactory](./datafactory-customization.md)   
 [Configurações do cliente necessárias](./required-client-settings.md)   
 [Noções básicas sobre o arquivo de personalização](./understanding-the-customization-file.md)