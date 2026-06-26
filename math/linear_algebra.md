
# Definitions

A vector is a matrix with only 1 column and n rows. 

\[
	\overline{x} = 
	\begin{bmatrix}
		1 \\
		2 \\
		3
	\end{bmatrix}
	\in \mathbb{R}^3
\]

The zero vector is denoted as follows

\[
	\overline{0} = 
	\begin{bmatrix}
		0 \\
		0 \\
		0
	\end{bmatrix}
	\in \mathbb{R}^3
\]

\underline{Vector Norms}: The $p$-norm of a vector is given by the formula: $||\overline{x}||_p = (\sum_{i=1}^n|x_i|^p)^{i/p}$

Ex: Consider the following vector:

\[
	\overline{x} = 
	\begin{bmatrix}
		1 \\
		2 \\
		3
	\end{bmatrix}
\]

\begin{itemize}
	\item When $p=2$: $||\overline{x}||_2 = \sqrt{1^2+2^2+3^2} = \sqrt{14}$ \hfill (Euclidean Norm)
	\item When $p=1$: $||\overline{x}||_1 = 1+2+3 = 6$ \hfill (Manhattan Norm)
\end{itemize}

\underline{Dot Product}: The definiton of a dot product (inner product) is:

\[ \overline{a} \cdot \overline{b} = \sum_{i=1}^na_ib_i = ||\overline{a}||||\overline{b}||cos\alpha\]

Where $\alpha$ is the angle between the two vectors.

\underline{Orthogonality}: When two nonzero vectors have a dot product of 0, they are orthogonal to each other.

Ex: 

\[
	\begin{aligned}
		\overline{a} &=
		\begin{bmatrix}
			2 \\
			1
		\end{bmatrix},
								 &
		\overline{b} &=
		\begin{bmatrix}
			-1 \\
			2
		\end{bmatrix}
	\end{aligned}
\]

Here, $\overline{a} \text{ and } \overline{b}$ are orthogonal.\\

\section{Matrices}
# Defnitions

$A \in \mathbb{R}^{n \times m}$ is a real-valued matrix with $n$ rows and $m$ columns.\\

# More Definitions
\begin{itemize}
	\item When $n=m, A$ is a square matrix
	\item A \underline{diagonal matrix} only has diagonal elements (e.g. D)
	\item The \underline{identity matrix} has all diagonal elements equal to 1
	\item Indexing a matrix can be written as: $[A]_{ij}=a_{ij}$
	\item Two matrices $A,B$ are equal iff $\forall i,j, a_{ij}=b_{ij}$
\end{itemize}

# Transpose of a Matrix
Let $A \in \mathbb{R}^{n \times m}$, then $A^T \in \mathbb{R}^{n \times m}$ where $[A^T]_{ij}=[A]_{ji}$\\

Ex:

\[
	\begin{aligned}
		A &=
		\begin{bmatrix}
			1 & 2\\
			3 & 4\\
			5 & 6\\
		\end{bmatrix}
			& \in \mathbb{R}^{3\times2},
			\quad
		A^T &=
		\begin{bmatrix}
			1 & 2 & 3\\
			4 & 5 & 6
		\end{bmatrix}
				& \in \mathbb{R}^{2\times3}
	\end{aligned}
\]

# Addition
$\text{If } A,B \in \mathbb{R}^{n \times m}, \text{ then } A \pm B \in \mathbb{R}^{n \times m} \text{ where } [A \pm B]_{ij} = a_{ij} \pm b_{ij}$\\
# Scalar Multiplication
$\text{If }k \in \mathbb{R} \text{ and } A \in \mathbb{R}^{n \times m}, \text{ then } kA \in \mathbb{R}^{n \times m} \text{ where } [kA]_{ij} = ka_{ij}$\\

# Matrix Multiplication 
$\text{If } A \in \mathbb{R}^{n \times m} \text { and } B \in \mathbb{R}^{m \times n}, \text{ then } AB \in \mathbb{R}^{n \times n} \text{ where } [AB]_{ij} = \sum_{k=1}^pa_{ik}b_{kj}$\\

Ex: 
\[
	\begin{aligned}
		AB &=
		\begin{bmatrix}
			a_1 & a_2\\
			a_3 & a_4\\
		\end{bmatrix}
		\begin{bmatrix}
			b_1 & b_2 & b_3\\
			b_4 & b_5 & b_6
		\end{bmatrix}
			 &=
			 \begin{bmatrix}
				 (a_1b_1 + a_2b_4) & (a_1b_2 + a_2b_5) & (a_1b_3 + a_2b_6)\\
				 (a_3b_1 + a_4b_4) & (a_3b_2 + a_4b_5) & (a_3b_3 + a_4b_6)\\
			 \end{bmatrix}
	\end{aligned}
\]


\subsubsection{Properties}
\begin{itemize}
	\item Associativity: $(AB)C = A(BC)$
	\item Destributivity: $A(B+C) = AB + AC$
	\item Identity: $AI_n = I_mA = A$
	\item Dot product: $\overline{x} \cdot \overline{y} = \overline{x}^T\overline{y}$
\end{itemize}

\subsubsection{Discussion Question 1}

Q. Write the linear system $x_1 + 2x_2 = 5, 3x_1 + 4x_2 = 6$ as an equationin matrix form, i.e. $A\overline{x}=\overline{b}$ for matrix $A$ and vector $b$.\\
A. 
\[
	\begin{aligned}
		\begin{bmatrix}
			1 & 2\\
			3 & 4
		\end{bmatrix}
			&
			\begin{bmatrix}
				x_1\\
				x_2
			\end{bmatrix}
			&=
			\begin{bmatrix}
				5\\
				6
			\end{bmatrix}
	\end{aligned}
\]

# Orthogonal Projection

Projecting a line ``straight down" at a 90-degree angle to the subspace. The vector $(v-Pv)$ is orthogonal to the subspace.

Formula to project $\overline{v}$ onto $\overline{s}$:
\[
	proj_{[\overline{s}]}(\overline{v}) = (\frac{\overline{v} \cdot \overline{s}}{\overline{s} \cdot \overline{s}})\overline{s}
\]

\subsubsection{Discussion Question 2}

Q. Project the vector $[2,3]^T$ onto the line $y=2x$.\\
A. 
\[
	\begin{aligned}
		\overline{v} &=
		\begin{bmatrix}
			2\\
			3
		\end{bmatrix},
								 &
		\overline{s} &=
		\begin{bmatrix}
			1\\
			2
		\end{bmatrix}\\
	\end{aligned}
\]
\[
	proj_{[\overline{s}]}(\overline{v}) = (\frac{2 \cdot 1 + 3 \cdot 2}{1 \cdot 1 + 2 \cdot 2})\overline{s} = (\frac{8}{5}) \ 
	\begin{bmatrix}
		1\\
		2
	\end{bmatrix}
	= 
	\begin{bmatrix}
		\frac{8}{5}\\
		\frac{16}{5}
	\end{bmatrix}
\]

# Matrix Calculus

# Gradiant

Consider a function $f: \mathbb{R}^n \rightarrow \mathbb{R}$, the gradient is:

\[\nabla_{\overline{x}}f = [\diffp{f}{{x_1}},\dots, \diffp{f}{{x_n}}]^T\]

provided that all the partial derivatives exist.\\

\underline{Properties}: Consider $f,g:\mathbb{R}^n\rightarrow \mathbb{R}$ and $k\in\mathbb{R}$

\begin{itemize}
	\item $\nabla kf=k\nabla f$
	\item $\nabla (f \pm g) = \nabla f \pm \nabla g$
	\item Product Rule: $\nabla (fg) = f \nabla g + (\nabla f)g$
\end{itemize}

\subsubsection{Discussion Question 3}

Q. Let $f(\overline{x}) = x_1^2 + 2x_2^2$. Find $\nabla f(\overline{x})$.\\
A. 
\[
	\begin{aligned}
		\nabla f(\overline{x}) &= 
		\begin{bmatrix}
			2x_1\\
			4x_2
		\end{bmatrix}
	\end{aligned}
\]

\subsubsection{Discussion Question 4}

Q. Let $f(\overline{x}) = \overline{x}^T\overline{x}.$ Find $\nabla f(\overline{x})$.\\
A. $f(\overline{x}) = x_1^2 + x_2^2 + \dots + x_n^2 \rightarrow \nabla f(\overline{x}) = [2x_1 + 2x_2 + \dots + 2x_n]^T = 2\overline{x}$

# Chain Rule

Given two differnetiable functions, $g:\mathbb{R}^n\rightarrow\mathbb{R}$ and $f:\mathbb{R}\rightarrow\mathbb{R}$. This specific application of the chain rule states: $\nabla (f \circ g)(\overline{x}) = f'(g(\overline{x})) \nabla g(\overline{x})$

\subsubsection{Discussion Question 5}

Q. Find $\frac{d}{dx}[\sqrt{3x^2-x}]$\\
A. Let $f(x) = x^2$ and $g(x) = 3x^2 - x$. Then
\[
	\begin{aligned}
		f'(x)&=\frac{1}{2}x^{-\frac{1}{2}}\\
		g'(x)&=6x-1\\
		f'(g(x))&=\frac{1}{2}(3x^2-x)^{-\frac{1}{2}}.
	\end{aligned}
\]

Therefore $\frac{d}{dx}[\sqrt{3x^2-x}] = f'(g(x))g'(x)=\frac{1}{2}(3x^2-x)^{-\frac 1 2}(6x-1)$

\subsubsection{Discussion Question 6}

Q. Find $\nabla h(\overline{x})$ where $h(\overline{x}) = (1 + \overline{\theta} \cdot \overline{x})^2$\\
A. Let $f(x) = x^2$ and $g(\overline{x}) = 1 + \overline{\theta} \cdot \overline{x}$. Then
\[
	\begin{aligned}
		f'(x)&=2x\\
		\nabla g(\overline{x})&=\overline{\theta}\\
		f'(g(\overline{x}))&=2(1 + \overline{\theta} \cdot \overline{x}).
	\end{aligned}
\]

Therefore $\nabla h(\overline{x}) = f'(g(\overline{x}))\nabla g(x)=2(1 + \overline{\theta} \cdot \overline{x})\overline{\theta}$


# Linear Classifiers

# Geometric Intuition

Given a set of points, we would like to create a boundary between different classes. This boundary can then be used to classify new data points. We can draw a linear decision boundary to separate space into a region where positive points lie and a region where negative points lie.\\

To classify a new point, we then only need to analyze which side of the decision boundary the new point lies on!

# Mathematical Formulation

The lines we can draw in the last subsection are more generally called \underline{hyperplanes}.\\

A hyperplane is mathematically defined by a parameter vector $\overline{\theta}$ such that all points on the hyperplane $\overline{x}$ satisfy $\overline{\theta}\cdot\overline{x}+b=0$ where $b$ is a constant offset.

\subsubsection{Discussion Question 7}

Q. Recall the relationship between the angle between $\overline{x}$ and $\overline{\theta}$ and the sign of $\overline{\theta}\cdot\overline{x}$. Derive the equation of the final classifier.\\
A. $h(\overline{x};\overline{\theta},b)=sign(\overline{\theta}\cdot\overline{x}+b)$. Basically, this is saying to find the classification of a new point $\overline{x}$, use the sign of $\overline{\theta}\cdot\overline{x}+b$. If the sign is positive, the the data point is positive, and vice versa. Idk how this works, but it works.
