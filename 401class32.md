# Permissions

- Together with authentication and throttling, permissions determine whether a request should be granted or denied accesss.
- Permission check are always run at they very start of the view, before any other code is allowed to proceed.
- Permission checks will typically use the authentication information in the `request.user` and `request.auth` properties to determine if the incoming request should be permitted.

## How permissions are determined

- Permissions in REST framework are always defined as a list of permission classes.
- If any permission check fails an `exceptions.PermissionDenied` or `exceptions.NotAuthenticated` exception will be raised, and the main body of the view will not run.
- when the permissions checks fail either a "403 forbidden" or a "401 Unauthorized" response will be returned.
- The request was successfully authenticated, but permission was denied -- HTTP 403 forbidden response will be returned.
- The request was not successfully authenticated, and the highest priority authentication class does not use `WWW-Authenticate` headers -- An HTTP 403 forbidden response will be returned.
- The request was not successfully authenticated, and the highest priority authentication clas does not use `WWW-Authenticate` headers -- An HTTP 401 Unauthorized response, with an appropricate `WWW-Authenticate` header will be returned.

## Object level permissions

- REST framework permissions also support object-level permissioning.
- OLP are used to determine if a user should be allowed to act on a particular object, which will typically be a model instance.
- OLP are run by REST FW generic view when `.get_object()` is called.
- As with view level permissions, an `exceptions.PermissionDenied` exception will be raised if the user is not allowed to act on the given object.

### Limitations of object level permissions

- generic views will not automatically apply object level permissions to each instance in a queryset when returning a list of object (performance reasons).
- When using OLP you'll want to filter the queryset appropiately, to ensure that users only have visibility onto instances that they are permitted to view.
- because the `get_object()` method is not called, OLP from the `has_object_permission()` method are not applied when creating objects.

## Setting the permission policy

- the defaul permission policy may be set globally using the `DEFAULT_PERMISSION_CLASSES` setting.
REST_FRAMEWORK = {
    'DEFAULT_PERMISSION_CLASSES': [
        'rest_framework.permissions.IsAuthenticated',
    ]
}

- you can also set the authentication policy on a per-view, or per-viewset basis, using teh `APIView` class-based views.
from rest_framework.permissions import IsAuthenticated
from rest_framework.response import Response
from rest_framework.views import APIView

class ExampleView(APIView):
    permission_classes = [IsAuthenticated]

    def get(self, request, format=None):
        content = {
            'status': 'request was permitted'
        }
        return Response(content)

## API reference

### AllowAny

- the `AllowAny` permission class will allow unrestricted access, regardless of if the request was authenticated or unauthenticated.

### IsAuthenticated

- the `IsAuthenticated` permission class will deny permission to any unauthenticated user, and allow permission otherwise.

### IsAdminUser

- the `IsAdminUser` permission class will deny permission to any user, unless `user.is_staff` is `True` in which case permission will be allowed.
- this permission is suitable if you want to your API to allow read permissions to anonymous users, and only allow write permissions to authenticated users.

## DjangoModelPermissions

- `POST` requests require the user to have the `add` permission on the model.
- `PUT` and `PATCH` request require the user to have the `change` permissions on the model.
- `DELETE` request require the user to have the `delete` permission on the model.

## DjangoObjectPermissions

- `POST` request require the user to have the `add` permission on the model instance.
- `PUT` and `PATCH` request require the user to have the `change` permission on model instance.
- `DELETE` request require the user to have the `delete` permission on the model instance.

## Custom permissions

- To implement a custom permission, override `BasePermission` and implement either, or  both, of the followfing methods:
- `.has_permission(self, request, view)`
- `.has_object_permission(self, request, view, ojb)`
- The methods should return `True` if the request should be granted access, and `False` otherwise.
- if you need to test if a reuqest is a read operation or a write operation , you should check the request method against the constant `SAFE_METHODS`, which is a tuple containing `GET`, `OPTIONS` AND `HEAD`.

