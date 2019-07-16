---
title: Escrevendo seu próprio manipulador personalizado | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory handler in RDS [ADO]
- customized handler in RDS [ADO]
ms.assetid: d447712a-e123-47b5-a3a4-5d366cfe8d72
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 98e2ec3538de68bffa5b22acc94dda3d81e5c6f2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67921883"
---
# <a name="writing-your-own-customized-handler"></a>Escrever seu próprio manipulador personalizado
Talvez você queira escrever seu próprio manipulador se você for um administrador de servidor IIS que queiram padrão dão suporte a RDS, mas mais controle sobre as solicitações do usuário e direitos de acesso.  
  
 MSDFMAP. Manipulador implementa o **IDataFactoryHandler** interface.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="idatafactoryhandler-interface"></a>Interface IDataFactoryHandler  
 Essa interface tem dois métodos, **GetRecordset** e **reconectar**. Ambos os métodos requerem que o [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propriedade ser definida como **adUseClient**.  
  
 Ambos os métodos usam argumentos que apareçam depois da primeira vírgula no "**manipulador =** " palavra-chave. Por exemplo, `"Handler=progid,arg1,arg2;"` irá passar uma cadeia de caracteres do argumento `"arg1,arg2"`, e `"Handler=progid"` irá passar um argumento nulo.  
  
## <a name="getrecordset-method"></a>Método GetRecordset  
 Este método consulta a fonte de dados e cria um novo [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto usando os argumentos fornecidos. O **conjunto de registros** deve ser aberto com **adLockBatchOptimistic** e não deve ser aberto de forma assíncrona.  
  
### <a name="arguments"></a>Argumentos  
 ***conn*** a cadeia de caracteres de conexão.  
  
 ***args*** os argumentos para o manipulador.  
  
 ***consulta*** o texto do comando para fazer uma consulta.  
  
 ***ppRS*** o ponteiro no qual o **Recordset** devem ser retornados.  
  
## <a name="reconnect-method"></a>Reconectar-se o método  
 Esse método atualiza a fonte de dados. Ele cria um novo [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto e anexa o determinado **conjunto de registros**.  
  
### <a name="arguments"></a>Argumentos  
 ***conn*** a cadeia de caracteres de conexão.  
  
 ***args*** os argumentos para o manipulador.  
  
 ***pRS*** um **Recordset** objeto.  
  
## <a name="msdfhdlidl"></a>msdfhdl.idl  
 Essa é a definição de interface para **IDataFactoryHandler** que aparece na **msdfhdl.idl** arquivo.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Seção conexão do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Seção de Logs do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [Seção SQL do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Seção de UserList do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [Personalização do DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Configurações de cliente necessárias](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Noções básicas sobre o arquivo de personalização](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)


