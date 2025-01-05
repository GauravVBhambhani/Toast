# Toast

## Description
`Toast` is a lightweight SwiftUI library that provides a simple way to display toast messages.

## Requirements

| Platform | Minimum Version |
|----------|-----------------|
| iOS      | 17.0            |
| macOS    | 14.0            |

## Get Started

1. Toast ViewModifier
```swift
import Toast
import SwiftUI

@MainActor
struct ExampleScreen {
    @State var isLoading: Bool = false
    @State var toastToPresent: Toast? = nil

    @Sendable func onTask() async {
        isLoading = true
        defer { isLoading = false }

        do {
            try await Task.sleep(for: .seconds(1))
            toastToPresent = .success(message: "Successfully did a thing!")
        } catch {
            toastToPresent = .error(message: "Failure to do a thing!")
        }
    }
}

extension ExampleScreen: View {
    var body: some View {
        VStack {
            Spacer()
        }
        .task(onTask)
        .toast($toastToPresent)
    }
}
```

2. Convenience Initializers

```swift
/// Extension to the Toast struct to provide convenience initializers for different types of toasts.
extension Toast {
    /// Creates a debug toast with a purple color and a debug icon.
    public static func debug(message: String) -> Toast {...}

    /// Creates an error toast with a red color and an error icon.
    public static func error(message: String) -> Toast {...}

    /// Creates an info toast with a blue color and an info icon.
    public static func info(message: String) -> Toast {...}

    /// Creates a notice toast with an orange color and a notice icon.
    public static func notice(message: String) -> Toast {...}

    /// Creates a success toast with a green color and a success icon.
    public static func success(message: String) -> Toast {...}

    /// Creates a warning toast with a yellow color and a warning icon.
    public static func warning(message: String) -> Toast {...}
}
```

3. Additional Options for Toast ViewModifier
```swift
/// Shows a toast with a provided configuration.
/// - Parameters:
///   - toast: A binding to the toast to display.
///   - edge: The edge of the screen where the toast appears.
///   - autoDismissable: Whether the toast should automatically dismiss.
///   - onDismiss: A closure to call when the toast is dismissed.
func toast(
    _ toast: Binding<Toast?>,
    edge: VerticalEdge = .top,
    autoDismissable: Bool = false,
    onDismiss: @escaping () -> Void = {}
) -> some View {...}
```
