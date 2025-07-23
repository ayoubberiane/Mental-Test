import { useState, useRef, useEffect } from 'react'
import { Button } from '@/components/ui/button.jsx'
import { Card, CardContent, CardDescription, CardHeader, CardTitle } from '@/components/ui/card.jsx'
import { Badge } from '@/components/ui/badge.jsx'
import { Separator } from '@/components/ui/separator.jsx'
import { Progress } from '@/components/ui/progress.jsx'
import { Home, TreePine, User, Palette, RotateCcw, Trash2, ChevronRight, Info, Star, Clock, Brush, Eye } from 'lucide-react'
import './App.css'

const phases = [
  {
    id: 'house',
    title: 'Draw a House',
    description: 'Draw a house as you imagine it. Include details like windows, doors, and surroundings. Let your intuition guide you.',
    icon: Home,
    color: 'from-blue-500 to-purple-600'
  },
  {
    id: 'tree',
    title: 'Draw a Tree',
    description: 'Draw a tree with roots, trunk, and branches. Show it as you envision a tree should look.',
    icon: TreePine,
    color: 'from-green-500 to-teal-600'
  },
  {
    id: 'person',
    title: 'Draw a Person',
    description: 'Draw a person of any age or gender. Include as much detail as feels natural to you.',
    icon: User,
    color: 'from-orange-500 to-red-600'
  }
]

const scientificInfo = {
  overview: "The House-Tree-Person (HTP) test is a projective psychological assessment developed by John Buck in 1948. It uses drawings to explore personality traits, emotional functioning, and psychological well-being.",
  validity: "Recent research (2022) shows mixed results regarding the HTP's validity. While some studies find it useful for therapeutic rapport-building, its diagnostic validity is questioned in modern psychological practice.",
  interpretation: {
    house: "Represents family relationships, security, and one's relationship with their home environment. Size, details, and placement can indicate feelings about family dynamics.",
    tree: "Symbolizes personal growth, life force, and connection to nature. The trunk represents ego strength, while branches may indicate social relationships.",
    person: "Reflects self-image, body awareness, and interpersonal relationships. Details like facial features, clothing, and posture provide insights into self-perception."
  },
  limitations: "The test lacks standardized scoring and interpretation guidelines. Results should be considered alongside other assessment tools and clinical observations."
}

function App() {
  const [currentPhase, setCurrentPhase] = useState(0)
  const [isDrawing, setIsDrawing] = useState(false)
  const [drawings, setDrawings] = useState([])
  const [insights, setInsights] = useState({
    drawingTime: 0,
    strokesMade: 0,
    colorsUsed: 1,
    canvasCoverage: 0
  })
  const [selectedColor, setSelectedColor] = useState('#000000')
  const [brushSize, setBrushSize] = useState(3)
  const [showScientificInfo, setShowScientificInfo] = useState(false)
  
  const canvasRef = useRef(null)
  const startTimeRef = useRef(null)
  const intervalRef = useRef(null)

  const colors = ['#000000', '#FF6B6B', '#4ECDC4', '#45B7D1', '#96CEB4', '#FFEAA7', '#DDA0DD', '#98D8C8']

  useEffect(() => {
    const canvas = canvasRef.current
    if (!canvas) return

    const ctx = canvas.getContext('2d')
    ctx.lineCap = 'round'
    ctx.lineJoin = 'round'
    ctx.fillStyle = '#ffffff'
    ctx.fillRect(0, 0, canvas.width, canvas.height)
  }, [currentPhase])

  useEffect(() => {
    if (isDrawing && !startTimeRef.current) {
      startTimeRef.current = Date.now()
      intervalRef.current = setInterval(() => {
        const elapsed = Math.floor((Date.now() - startTimeRef.current) / 1000)
        setInsights(prev => ({ ...prev, drawingTime: elapsed }))
      }, 1000)
    } else if (!isDrawing && intervalRef.current) {
      clearInterval(intervalRef.current)
    }

    return () => {
      if (intervalRef.current) clearInterval(intervalRef.current)
    }
  }, [isDrawing])

  const startDrawing = (e) => {
    const canvas = canvasRef.current
    const rect = canvas.getBoundingClientRect()
    const x = e.clientX - rect.left
    const y = e.clientY - rect.top

    setIsDrawing(true)
    const ctx = canvas.getContext('2d')
    ctx.beginPath()
    ctx.moveTo(x, y)
  }

  const draw = (e) => {
    if (!isDrawing) return

    const canvas = canvasRef.current
    const rect = canvas.getBoundingClientRect()
    const x = e.clientX - rect.left
    const y = e.clientY - rect.top

    const ctx = canvas.getContext('2d')
    ctx.lineWidth = brushSize
    ctx.strokeStyle = selectedColor
    ctx.lineTo(x, y)
    ctx.stroke()

    setInsights(prev => ({ ...prev, strokesMade: prev.strokesMade + 1 }))
  }

  const stopDrawing = () => {
    setIsDrawing(false)
  }

  const clearCanvas = () => {
    const canvas = canvasRef.current
    const ctx = canvas.getContext('2d')
    ctx.fillStyle = '#ffffff'
    ctx.fillRect(0, 0, canvas.width, canvas.height)
    setInsights(prev => ({ ...prev, strokesMade: 0, canvasCoverage: 0 }))
  }

  const nextPhase = () => {
    if (currentPhase < phases.length - 1) {
      const canvas = canvasRef.current
      const dataURL = canvas.toDataURL()
      setDrawings(prev => [...prev, { phase: currentPhase, data: dataURL }])
      setCurrentPhase(currentPhase + 1)
      setInsights({ drawingTime: 0, strokesMade: 0, colorsUsed: 1, canvasCoverage: 0 })
      startTimeRef.current = null
    } else {
      // Complete analysis
      const canvas = canvasRef.current
      const dataURL = canvas.toDataURL()
      setDrawings(prev => [...prev, { phase: currentPhase, data: dataURL }])
      alert('Analysis complete! In a real implementation, this would provide detailed psychological insights.')
    }
  }

  const currentPhaseData = phases[currentPhase]
  const PhaseIcon = currentPhaseData.icon

  return (
    <div className="min-h-screen bg-gradient-to-br from-slate-50 to-blue-50">
      {/* Header */}
      <header className="bg-white/80 backdrop-blur-sm border-b border-slate-200 sticky top-0 z-50">
        <div className="max-w-7xl mx-auto px-4 py-4">
          <div className="flex items-center justify-between">
            <div className="flex items-center space-x-3">
              <div className="w-10 h-10 bg-gradient-to-br from-purple-500 to-blue-600 rounded-lg flex items-center justify-center">
                <Home className="w-5 h-5 text-white" />
              </div>
              <div>
                <h1 className="text-2xl font-bold bg-gradient-to-r from-purple-600 to-blue-600 bg-clip-text text-transparent">
                  House Tree Person Test
                </h1>
                <p className="text-sm text-slate-600">Discover your psychological landscape through intuitive drawing</p>
              </div>
            </div>
            <Button
              variant="outline"
              onClick={() => setShowScientificInfo(!showScientificInfo)}
              className="flex items-center space-x-2"
            >
              <Info className="w-4 h-4" />
              <span>Scientific Background</span>
            </Button>
          </div>
        </div>
      </header>

      {/* Scientific Information Panel */}
      {showScientificInfo && (
        <div className="bg-blue-50 border-b border-blue-200">
          <div className="max-w-7xl mx-auto px-4 py-6">
            <Card>
              <CardHeader>
                <CardTitle className="flex items-center space-x-2">
                  <Star className="w-5 h-5 text-yellow-500" />
                  <span>Scientific Background & Validity</span>
                </CardTitle>
              </CardHeader>
              <CardContent className="space-y-4">
                <div>
                  <h4 className="font-semibold text-slate-800 mb-2">Overview</h4>
                  <p className="text-slate-600 text-sm">{scientificInfo.overview}</p>
                </div>
                <Separator />
                <div>
                  <h4 className="font-semibold text-slate-800 mb-2">Current Validity Status</h4>
                  <div className="flex items-center space-x-2 mb-2">
                    <Badge variant="secondary">Research-Based</Badge>
                    <Badge variant="outline">Mixed Evidence</Badge>
                  </div>
                  <p className="text-slate-600 text-sm">{scientificInfo.validity}</p>
                </div>
                <Separator />
                <div>
                  <h4 className="font-semibold text-slate-800 mb-2">Interpretation Guidelines</h4>
                  <div className="grid md:grid-cols-3 gap-4">
                    <div className="space-y-2">
                      <div className="flex items-center space-x-2">
                        <Home className="w-4 h-4 text-blue-500" />
                        <span className="font-medium text-sm">House</span>
                      </div>
                      <p className="text-xs text-slate-600">{scientificInfo.interpretation.house}</p>
                    </div>
                    <div className="space-y-2">
                      <div className="flex items-center space-x-2">
                        <TreePine className="w-4 h-4 text-green-500" />
                        <span className="font-medium text-sm">Tree</span>
                      </div>
                      <p className="text-xs text-slate-600">{scientificInfo.interpretation.tree}</p>
                    </div>
                    <div className="space-y-2">
                      <div className="flex items-center space-x-2">
                        <User className="w-4 h-4 text-orange-500" />
                        <span className="font-medium text-sm">Person</span>
                      </div>
                      <p className="text-xs text-slate-600">{scientificInfo.interpretation.person}</p>
                    </div>
                  </div>
                </div>
                <Separator />
                <div>
                  <h4 className="font-semibold text-slate-800 mb-2">Important Limitations</h4>
                  <p className="text-slate-600 text-sm">{scientificInfo.limitations}</p>
                </div>
              </CardContent>
            </Card>
          </div>
        </div>
      )}

      {/* Progress Bar */}
      <div className="max-w-7xl mx-auto px-4 py-4">
        <div className="flex items-center justify-between mb-2">
          <span className="text-sm font-medium text-slate-700">Progress</span>
          <span className="text-sm text-slate-500">{currentPhase + 1} of {phases.length}</span>
        </div>
        <Progress value={(currentPhase / (phases.length - 1)) * 100} className="h-2" />
      </div>

      {/* Main Content */}
      <div className="max-w-7xl mx-auto px-4 pb-8">
        <div className="grid lg:grid-cols-3 gap-6">
          {/* Drawing Canvas */}
          <div className="lg:col-span-2">
            <Card className="overflow-hidden">
              <CardHeader className={`bg-gradient-to-r ${currentPhaseData.color} text-white`}>
                <div className="flex items-center space-x-3">
                  <PhaseIcon className="w-6 h-6" />
                  <div>
                    <CardTitle>Phase {currentPhase + 1}: {currentPhaseData.title}</CardTitle>
                    <CardDescription className="text-white/80">
                      {currentPhaseData.description}
                    </CardDescription>
                  </div>
                </div>
              </CardHeader>
              <CardContent className="p-6">
                {/* Drawing Tools */}
                <div className="flex flex-wrap items-center gap-4 mb-4">
                  <div className="flex items-center space-x-2">
                    <Palette className="w-4 h-4 text-slate-600" />
                    <span className="text-sm font-medium">Color:</span>
                    <div className="flex space-x-1">
                      {colors.map((color) => (
                        <button
                          key={color}
                          onClick={() => setSelectedColor(color)}
                          className={`w-6 h-6 rounded-full border-2 ${
                            selectedColor === color ? 'border-slate-400' : 'border-slate-200'
                          }`}
                          style={{ backgroundColor: color }}
                        />
                      ))}
                    </div>
                  </div>
                  <div className="flex items-center space-x-2">
                    <Brush className="w-4 h-4 text-slate-600" />
                    <span className="text-sm font-medium">Size:</span>
                    <input
                      type="range"
                      min="1"
                      max="10"
                      value={brushSize}
                      onChange={(e) => setBrushSize(parseInt(e.target.value))}
                      className="w-20"
                    />
                    <span className="text-sm text-slate-500">{brushSize}px</span>
                  </div>
                  <div className="flex space-x-2">
                    <Button variant="outline" size="sm" onClick={clearCanvas}>
                      <Trash2 className="w-4 h-4 mr-1" />
                      Clear
                    </Button>
                  </div>
                </div>

                {/* Canvas */}
                <div className="border-2 border-slate-200 rounded-lg overflow-hidden bg-white">
                  <canvas
                    ref={canvasRef}
                    width={600}
                    height={400}
                    className="w-full h-auto cursor-crosshair"
                    onMouseDown={startDrawing}
                    onMouseMove={draw}
                    onMouseUp={stopDrawing}
                    onMouseLeave={stopDrawing}
                  />
                </div>

                {/* Continue Button */}
                <div className="mt-6 flex justify-end">
                  <Button
                    onClick={nextPhase}
                    className={`bg-gradient-to-r ${currentPhaseData.color} hover:opacity-90 text-white`}
                  >
                    {currentPhase < phases.length - 1 ? (
                      <>
                        Continue to {phases[currentPhase + 1].title}
                        <ChevronRight className="w-4 h-4 ml-1" />
                      </>
                    ) : (
                      'Complete Analysis'
                    )}
                  </Button>
                </div>
              </CardContent>
            </Card>
          </div>

          {/* Insights Panel */}
          <div className="space-y-6">
            <Card>
              <CardHeader>
                <CardTitle className="flex items-center space-x-2">
                  <Eye className="w-5 h-5 text-purple-500" />
                  <span>Live Insights</span>
                </CardTitle>
              </CardHeader>
              <CardContent className="space-y-4">
                <div className="space-y-3">
                  <div className="flex justify-between items-center">
                    <div className="flex items-center space-x-2">
                      <Clock className="w-4 h-4 text-blue-500" />
                      <span className="text-sm font-medium">Drawing Time:</span>
                    </div>
                    <Badge variant="secondary">{insights.drawingTime}s</Badge>
                  </div>
                  <div className="flex justify-between items-center">
                    <div className="flex items-center space-x-2">
                      <Brush className="w-4 h-4 text-green-500" />
                      <span className="text-sm font-medium">Strokes Made:</span>
                    </div>
                    <Badge variant="secondary">{insights.strokesMade}</Badge>
                  </div>
                  <div className="flex justify-between items-center">
                    <div className="flex items-center space-x-2">
                      <Palette className="w-4 h-4 text-orange-500" />
                      <span className="text-sm font-medium">Colors Used:</span>
                    </div>
                    <Badge variant="secondary">{insights.colorsUsed}</Badge>
                  </div>
                  <div className="flex justify-between items-center">
                    <div className="flex items-center space-x-2">
                      <Eye className="w-4 h-4 text-purple-500" />
                      <span className="text-sm font-medium">Canvas Coverage:</span>
                    </div>
                    <Badge variant="secondary">{insights.canvasCoverage}%</Badge>
                  </div>
                </div>
              </CardContent>
            </Card>

            {/* Phase Navigation */}
            <Card>
              <CardHeader>
                <CardTitle>Test Phases</CardTitle>
              </CardHeader>
              <CardContent>
                <div className="space-y-3">
                  {phases.map((phase, index) => {
                    const Icon = phase.icon
                    return (
                      <div
                        key={phase.id}
                        className={`flex items-center space-x-3 p-3 rounded-lg border ${
                          index === currentPhase
                            ? 'border-purple-200 bg-purple-50'
                            : index < currentPhase
                            ? 'border-green-200 bg-green-50'
                            : 'border-slate-200 bg-slate-50'
                        }`}
                      >
                        <div
                          className={`w-8 h-8 rounded-full flex items-center justify-center ${
                            index === currentPhase
                              ? 'bg-purple-500 text-white'
                              : index < currentPhase
                              ? 'bg-green-500 text-white'
                              : 'bg-slate-300 text-slate-600'
                          }`}
                        >
                          <Icon className="w-4 h-4" />
                        </div>
                        <div className="flex-1">
                          <div className="font-medium text-sm">{phase.title}</div>
                          <div className="text-xs text-slate-500">
                            {index === currentPhase
                              ? 'Current'
                              : index < currentPhase
                              ? 'Completed'
                              : 'Upcoming'}
                          </div>
                        </div>
                      </div>
                    )
                  })}
                </div>
              </CardContent>
            </Card>
          </div>
        </div>
      </div>
    </div>
  )
}

export default App

