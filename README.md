# Placing-multiple-AR-models-SwiftUI-RealityKit
AR model with a cube and a sphere placed
# The first part
![IMG_1220](https://github.com/S-way520/Placing-multiple-AR-models-SwiftUI-RealityKit/assets/95877651/cbaea7f7-dcfb-4d74-987d-63f577cd4881)
# The sceond part
Code file 1
```swift
import SwiftUI
@main
struct MyApp: App {
    var body: some Scene {
        WindowGroup {
            Reality()
        }
    }
}
```
Codel file 2
```swift
import SwiftUI
import RealityKit
struct Reality: View {
    var body: some View {
        ARViewContainer().edgesIgnoringSafeArea(.all)
    }
}
struct ARViewContainer: UIViewRepresentable {
    func makeUIView(context: Context) -> ARView {
        let arView = ARView(frame: .zero, cameraMode: .ar, automaticallyConfigureSession: true)
        let anchorEntity = AnchorEntity(plane: .horizontal)
        let box = MeshResource.generateBox(size: 0.2/2, cornerRadius: 0.05/5)//1
        let sphere = MeshResource.generateSphere(radius: 0.2/4)//2
        //还有Plane(平面)等
        let material = SimpleMaterial(color: .blue, isMetallic: true)//Color
        let AR1entity = ModelEntity(mesh: box, materials: [material])//1
        let AR2entity = ModelEntity(mesh: sphere, materials: [material])//2
        AR2entity.position = simd_make_float3(0,0.2/2,0)//position
        anchorEntity.addChild(AR1entity)//add1
        anchorEntity.addChild(AR2entity)//add2
        arView.scene.anchors.append(anchorEntity)
        return arView
    }
    func updateUIView(_ uiView: ARView, context: Context) {
    }
}
```
